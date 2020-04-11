---
date: "2016-12-21T00:00:00Z"
tags:
- magento2
- nginx
title: Magento 2.1.3 Upgrade Static Files Not Loading
---
Magento just released an update to the latest version of their ecommerce platform to up the version from 2.1.2 to 2.1.3. There are a few differences between the versions, and one of those differences relates to the handling of the static files and what method is used to bust the cache of browsers to ensure users get the latest code whenever changes are deployed. Unfortunately, this upgrade by default breaks sites that aren't aware of the changes needed to make this work properly.

While these changes affect sites using both nginx and Apache as their webservers, I am currently using nginx with my Magento 2 installations, so I'll only outline the changes needed to the example nginx configuration files.

The way to know for sure that your site is in need of this fix is that when you try to load any frontend pages or admin pages, there is a lack of styling and functionality to make the site work. When you look in the web inspector of your favorite browser, you will see lots of 404 File Not Found errors for the CSS and JavaScript files. These files will have in their path `version23423423` appear. Effectively, this is the way that Magento busts the cache as the number after `version` is generated each time the static files are updated, ensuring you get the latest version.

If you look at the older version of the `nginx.conf.sample`, you will find the following setup under the section that configures the loading of the static files:

```nginx
location /static/ {
    # Uncomment the following line in production mode
    # expires max;

    location ~* \.(ico|jpg|jpeg|png|gif|svg|js|css|swf|eot|ttf|otf|woff|woff2)$ {
      add_header Cache-Control "public";
      add_header X-Frame-Options "SAMEORIGIN";
      expires +1y;

      if (!-f $request_filename) {
        rewrite ^/static/(version\d*/)?(.*)$ /static.php?resource=$2 last;
      }
    }

    location ~* \.(zip|gz|gzip|bz2|csv|xml)$ {
      add_header Cache-Control "no-store";
      add_header X-Frame-Options "SAMEORIGIN";
      expires off;

      if (!-f $request_filename) {
         rewrite ^/static/(version\d*/)?(.*)$ /static.php?resource=$2 last;
      }
    }

    if (!-f $request_filename) {
      rewrite ^/static/(version\d*/)?(.*)$ /static.php?resource=$2 last;
    }

    add_header X-Frame-Options "SAMEORIGIN";
}
```

One thing that becomes ovbious when you take a look at this and compare it to the `nginx.conf.sample` that Magento 2.1.3 installs, and you will see that there is a significant change after the section to uncomment for production mode.

```nginx
location /static/ {
    # Uncomment the following line in production mode
    # expires max;

    # Remove signature of the static files that is used to overcome the browser cache
    location ~ ^/static/version {
        rewrite ^/static/(version\d*/)?(.*)$ /static/$2 last;
    }

    location ~* \.(ico|jpg|jpeg|png|gif|svg|js|css|swf|eot|ttf|otf|woff|woff2)$ {
        add_header Cache-Control "public";
        add_header X-Frame-Options "SAMEORIGIN";
        expires +1y;

        if (!-f $request_filename) {
            rewrite ^/static/(version\d*/)?(.*)$ /static.php?resource=$2 last;
        }
    }
    location ~* \.(zip|gz|gzip|bz2|csv|xml)$ {
        add_header Cache-Control "no-store";
        add_header X-Frame-Options "SAMEORIGIN";
        expires    off;

        if (!-f $request_filename) {
           rewrite ^/static/(version\d*/)?(.*)$ /static.php?resource=$2 last;
        }
    }
    if (!-f $request_filename) {
        rewrite ^/static/(version\d*/)?(.*)$ /static.php?resource=$2 last;
    }
    add_header X-Frame-Options "SAMEORIGIN";
}
```

To fix the issue, you can either take the sample config file and port all your changes and customizations to it, or more easiliy, overwrite your section that currently has been handling the `/static/` requests with what is seen above or at the [Magento 2 repository](https://github.com/magento/magento2/blob/2.1/nginx.conf.sample).
