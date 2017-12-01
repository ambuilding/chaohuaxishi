---
layout: post
title: Elasticsearch-PHP
---

### Hi

- `composer require elasticsearch/elasticsearch`

- Index a document: index, type, id and a document body.
- Configuration
- Elasticsearch-PHP uses an interchangeable HTTP transport layer called RingPHP.
- "future" or "async" mode. `'future' => 'lazy'` PHP is fundamentally single-threaded, however libcurl provides functionality called the "multi interface".  With the multi interface, the time to execute n requests is the latency of the slowest request. Furthermore, the multi-interface allows requests to different hosts simultaneously, which means the Elasticsearch-PHP client can more effectively utilize your full cluster.





### Link
- [Elasticsearch-PHP](https://www.elastic.co/guide/en/elasticsearch/client/php-api/current/index.html)
- [How to integrate your Laravel app with Elasticsearch](https://blog.madewithlove.be/post/how-to-integrate-your-laravel-app-with-elasticsearch/) `docker run -d -p 9200:9200 elasticsearch`
- [Laravel scout customer driven](https://gist.github.com/lukepolo/b63d303b076a7cd58bbaa54b3b9f0370)
- [ErickTamayo/laravel-scout-elastic](https://github.com/ErickTamayo/laravel-scout-elastic)
- [YABhq/laravel-scout-mysql-driver](https://github.com/YABhq/laravel-scout-mysql-driver)
- [lukepolo](https://github.com/lukepolo)
- [Learning Elasticsearch with Laravel](https://michaelstivala.com/learning-elasticsearch-with-laravel/)
- [Freek Van der Herten, a partner & developer at Spatie](https://murze.be/me)

