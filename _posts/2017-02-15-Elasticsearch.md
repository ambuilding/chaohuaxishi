---
layout: post
title: Elasticsearch
---

### Getting started
- `docker.elastic.co/elasticsearch/elasticsearch   6.0.0               b685d8dba1a4        2 weeks ago         537MB
`
- `docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:6.0.0
`
- `docker run -d -p 9200:9200 elasticsearch`

- [Docker docs elasticsearch](https://docs.docker.com/samples/library/elasticsearch/)

- Elasticsearch is a highly scalable open-source full-text search and analytics engine. It allows us to store, search, and analyze big volumes of data quickly and in near real time. (Log and search)

### Foundation
- It is important to understand that once you get your search results back, Elasticsearch is completely done with the request and does not maintain any kind of server-side resources or open cursors into your results.
- This is in stark contrast to many other platforms such as SQL wherein you may initially get a partial subset of your query results up-front and then you have to continuously go back to the server if you want to fetch (or page through) the rest of the results using some kind of stateful server-side cursor.

### Installation: Java and Elasticsearch; Running node. (or Docker)

```
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.0.0.tar.gz
tar -xvf elasticsearch-6.0.0.tar.gz
bin/elasticsearch
curl http://localhost:9200/
```

### Exploring the Cluster
- Health `curl -XGET 'localhost:9200/_cat/health?v&pretty'`
- Get a list of nodes in our cluster `curl -XGET 'localhost:9200/_cat/nodes?v&pretty'`
- List all indices `curl -XGET 'localhost:9200/_cat/indices?v&pretty'`
- Create an index `curl -XPUT 'localhost:9200/customer?pretty&pretty'`
- Index and query a document

```
curl -XPUT 'localhost:9200/customer/doc/1?pretty&pretty' -H 'Content-Type: application/json' -d'
{
	"name": "John Doe"
}
'
```

- Retrieve the document that we just indexed `curl -XGET 'localhost:9200/customer/doc/1?pretty&pretty'`

- Delete an index `curl -XDELETE 'localhost:9200/customer?pretty&pretty'`
- A pattern of how we access data in Elasticsearch `<REST Verb> /<Index>/<Type>/<ID>`

### Modifying the Data
- (Index and query a document). Using the POST verb instead of PUT since we didn’t specify an ID.

```
curl -XPOST 'localhost:9200/customer/doc?pretty&pretty' -H 'Content-Type: application/json' -d'
{
  "name": "Jane Doe"
}
'
```

- Updating documents

```
curl -XPOST 'localhost:9200/customer/doc/1/_update?pretty&pretty' -H 'Content-Type: application/json' -d'
{
  "doc": { "name": "Jane Doe", "age": 20 }
}
'

{
  "script" : "ctx._source.age += 5"
}

```
- Deleting documents `curl -XDELETE 'localhost:9200/customer/doc/2?pretty&pretty'`
- Batch Processing

```
curl -XPOST 'localhost:9200/customer/doc/_bulk?pretty&pretty' -H 'Content-Type: application/json' -d'
{"index":{"_id":"1"}}
{"name": "John Doe" }
{"index":{"_id":"2"}}
{"name": "Jane Doe" }
'

curl -XPOST 'localhost:9200/customer/doc/_bulk?pretty&pretty' -H 'Content-Type: application/json' -d'
{"update":{"_id":"1"}}
{"doc": { "name": "John Doe becomes Jane Doe" } }
{"delete":{"_id":"2"}}
'
```

### Exploring the Data

- Loading the sample dataset

```
curl -H "Content-Type: application/json" -XPOST 'localhost:9200/bank/account/_bulk?pretty&refresh' --data-binary "@accounts.json"
curl 'localhost:9200/_cat/indices?v'
```

- The search API

```
# REST request URI
curl -XGET 'localhost:9200/bank/_search?q=*&sort=account_number:asc&pretty&pretty'

#  REST request body
curl -XGET 'localhost:9200/bank/_search?pretty' -H 'Content-Type: application/json' -d'
{
  "query": { "match_all": {} },
  "sort": [
    { "account_number": "asc" }
  ]
}
'
```

- Introducing the query language - a JSON-style domain-specific language

```
# query
{
  "query": { "match_all": {} }
  "size": 1

  "from": 10,
  "size": 10

  "sort": { "balance": { "order": "desc" } }
}
'
```

- Executing searches

```
# Fields
"_source": ["account_number", "balance"]

# search a specific field
"query": { "match": { "account_number": 20 } }
"query": { "match": { "address": "mill" } }
"query": { "match": { "address": "mill lane" } }

# The bool must clause specifies all the queries that must be true for a document to be considered a match.
"query": {
    "bool": {
      "must": [
        { "match": { "address": "mill" } },
        { "match": { "address": "lane" } }
      ]
    }
  }

# The bool should clause specifies a list of queries either of which must be true for a document to be considered a match.
	"bool": { "should": [] }

# The bool must_not clause specifies a list of queries none of which must be true for a document to be considered a match.
	"bool": { "must_not": [] }

# Combine must, should, and must_not clauses simultaneously inside a bool query.
    "bool": {
      "must": [
        { "match": { "age": "40" } }
      ],
      "must_not": [
        { "match": { "state": "ID" } }
      ]
    }
```

- Executing filters

```
# range query, numeric / date filtering
{
  "query": {
    "bool": {
      "must": { "match_all": {} },
      "filter": {
        "range": {
          "balance": {
            "gte": 20000,
            "lte": 30000
          }
        }
      }
    }
  }
}
```

- Executing aggregations

```
# Groups all the accounts by state, and then returns the top 10 (default) states sorted by count descending (also default)
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}

# In SQL, similar in concept to
SELECT state, COUNT(*) FROM bank GROUP BY state ORDER BY COUNT(*) DESC

# Calculate the average account balance by state.
      "aggs": {
        "average_balance": {
          "avg": {
            "field": "balance"
          }
        }
       }

# Sort on the average balance in descending order
		"field": "state.keyword",
		"order": {
          "average_balance": "desc"
        }

# Group by age brackets (ages 20-29, 30-39, and 40-49), then by gender, and then finally get the average account balance, per age bracket, per gender
{
  "size": 0,
  "aggs": {
    "group_by_age": {
      "range": {
        "field": "age",
        "ranges": [
          {
            "from": 20,
            "to": 30
          },
          {
            "from": 30,
            "to": 40
          },
          {
            "from": 40,
            "to": 50
          }
        ]
      },
      "aggs": {
        "group_by_gender": {
          "terms": {
            "field": "gender.keyword"
          },
          "aggs": {
            "average_balance": {
              "avg": {
                "field": "balance"
              }
            }
          }
        }
      }
    }
  }
}
```

### Link

- [Elasticsearch Reference [6.0]](https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started.html)
- [Starting Elasticsearch / Kibana / X-Pack](https://www.elastic.co/start)
- [ruanyifeng](http://www.ruanyifeng.com/blog/2017/08/elasticsearch.html)
- [http://www.jianshu.com/p/05cff717563c](http://www.jianshu.com/p/05cff717563c)
- [Elasticsearch with Docker](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#_image_types)


### Text search
- Analyze
- tokens breakdown of the text. (By word)
- query: term and match

- split the string into chunks (tokenizing)
- apply some formatting on each of those tokens (lowercasing, convert special chars, …)
- the default behavior is described by the standard analyzer. It will split the texts by word and those words will be lowercased.

- Link
  - [Basic understanding of text search in elasticsearch](https://blog.madewithlove.be/post/basic-understanding-of-text-search/)
  - [Analyze-Doc](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-analyze.html)
  - [Validate API](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-validate.html#search-validate)
  - [Strings are dead, long live strings!](https://www.elastic.co/blog/strings-are-dead-long-live-strings)


### With Security

- Generate default passwords... `bin/x-pack/setup-passwords auto`


### Elasticsearch-PHP

- `composer require elasticsearch/elasticsearch`

- Index a document: index, type, id and a document body.
- Configuration
- Elasticsearch-PHP uses an interchangeable HTTP transport layer called RingPHP.
- "future" or "async" mode. `'future' => 'lazy'` PHP is fundamentally single-threaded, however libcurl provides functionality called the "multi interface".  With the multi interface, the time to execute n requests is the latency of the slowest request. Furthermore, the multi-interface allows requests to different hosts simultaneously, which means the Elasticsearch-PHP client can more effectively utilize your full cluster.





### Link
- [Docs Elasticsearch-PHP](https://www.elastic.co/guide/en/elasticsearch/client/php-api/current/index.html)
- [How to integrate your Laravel app with Elasticsearch](https://blog.madewithlove.be/post/how-to-integrate-your-laravel-app-with-elasticsearch/) `docker run -d -p 9200:9200 elasticsearch`
- [Laravel scout customer driven](https://gist.github.com/lukepolo/b63d303b076a7cd58bbaa54b3b9f0370)
- [ErickTamayo/laravel-scout-elastic](https://github.com/ErickTamayo/laravel-scout-elastic)
- [YABhq/laravel-scout-mysql-driver](https://github.com/YABhq/laravel-scout-mysql-driver)
- [lukepolo](https://github.com/lukepolo)
- [Learning Elasticsearch with Laravel](https://michaelstivala.com/learning-elasticsearch-with-laravel/)
- [Freek Van der Herten, a partner & developer at Spatie](https://murze.be/me)

