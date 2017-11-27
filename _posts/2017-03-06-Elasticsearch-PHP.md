---
layout: post
title: Elasticsearch-PHP
---

### Hi

- Index a document: index, type, id and a document body.
- Configuration
- Elasticsearch-PHP uses an interchangeable HTTP transport layer called RingPHP.
- "future" or "async" mode. `'future' => 'lazy'` PHP is fundamentally single-threaded, however libcurl provides functionality called the "multi interface".  With the multi interface, the time to execute n requests is the latency of the slowest request. Furthermore, the multi-interface allows requests to different hosts simultaneously, which means the Elasticsearch-PHP client can more effectively utilize your full cluster.





### Link
- [Elasticsearch-PHP](https://www.elastic.co/guide/en/elasticsearch/client/php-api/current/index.html)
