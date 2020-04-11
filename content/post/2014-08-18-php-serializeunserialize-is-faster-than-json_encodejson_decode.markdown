---
date: "2014-08-18T01:18:13Z"
tags:
- performance
- php
title: PHP serialize/unserialize is faster than json_encode/json_decode
---

One of the things that I tend to focus on with a website is how quickly everything loads and executes. However, that focus can sometimes get to be a bit too narrow, only considering the performance of those resources that are required for the initial page load, and not for other dynamic aspects of the site. We recently implemented [New Relic](http://www.newrelic.com) on one site, and gained much insight into how long each aspect of our site took to load, and how long each of the most popular requests took to execute.

Surprisingly, one particular request that we use to update the pricing without accessing the database was taking as long as other requests that had to access the database multiple times to complete the request. At that point, I got curious and began timing each line of code to see just how long each operation took to execute. The first thing I found was that it took about 75% of the total time to open the stored json file and use `json_decode` to parse it into a PHP object. As a result, I started looking at other methods of persisting data to disk, and stumbled across the `serialize`/`deserialize` combination and that it may take a bit longer to `serialize` the data, but the `desearialize` function should be much faster. After testing, this seemed to take what previously was a 100ms operation down to around 50ms.

Luckily, that was not the end of the options for optimizing the execution of this request. It turned out that many of the requests did not need the entire payload of the data that was in the serialized file and only delivering the needed data could reduce the download size by almost half. Interestingly enough, when we made this change, the download time for this request did not change by 50%, but the real change was on the server side. Instead of `deserialize` for the entire dataset, we limited the data in the file that we `serialize` and `deserialize`, making that process faster, and it turns out that it took the average time required down to about 25ms.

If you have the correct tooling, you really can make some significant performance improvements without changing the logical design of your application.