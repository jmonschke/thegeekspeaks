---
date: "2015-03-19T01:25:00Z"
tags:
- windows-7
- microsoft
- python
- web-development
- apache
title: Run Multiple Python mod_wsgi Websites With Apache On Windows
---

Yes, this sounds completely crazy, but there is a semi-valid need to do this, unfortunately. However, when you need to run multiple Python websites on Apache on Windows via mod_wsgi, it quickly becomes apparent that using the typical `<VirtualHost>` configuration options do not work as expected.

When you try to do it with a `<VirtualHost>` configuration, you will be unable to setup a separate `WSGIPythonPath` configuration setting per virtual host, as that configuration directive is not allowed within a `<VirtualHost>` node. Instead, you have a single `WSGIPythonPath` for your entire Apache instance. 

If you determine that a single `WSGIPythonPath` will not work for each website you are hosting separately, the only solution I have found so far is to setup multiple Apache services, each running on its own IP Address/Port combination. If you are running Apache 2.2 on a 64-bit version of Windows, you can run the following to setup a new Apache service:

```
"%SystemDrive%\Program Files(x86)\Apache Software Group\Apache 2.2\bin\httpd.exe" -k install -n "Apache 2.2-Secondary" -f "%SystemDrive%\Program Files(x86)\Apache Software Group\Apache 2.2\conf\httpd_secondary.conf"
```

Once the service is installed properly, you just need to make sure to put your configuration options in `httpd_secondary.conf` and then start the service, and you now have two separate Apache webservers running two separate mod_wsgi Python websites on the same Windows computer.