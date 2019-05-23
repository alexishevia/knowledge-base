# Elasticsearch v1.6

## Indexing a document
`PUT /<index>/<type>/<id>`

Example:
```
curl -XPUT http://localhost:9200/megacorp/employee/1 -d '
{
    "first_name": "John",
    "last_name": "Smith",
    "age": 25,
    "interests": ["sports", "music"]
}'
```

Tips:
- use `?op_type=create` or `/_create` to make sure the document is not updated,
  only created
- use `?version=N` to make sure you won't override previous changes
- you can run [Bulk updates](https://goo.gl/i2rlUZ)

## Partial update

- Using a partial document
  ```
  POST /<index>/<type>/<id>/_update

  { "doc": { new data } }
  ```

  Example:
  ```
  curl -XPOST http://localhost:9200/megacorp/employee/1/_update -d '
  {
    "doc": {
      "first_name": "Joe"
    }
  }'
  ```

- Using a script (scripted updates)
  ```
  POST /<index>/<type>/<id>/_update

  { "script": <update script> }
  ```

  Example:
  ```
  curl -XPOST http://localhost:9200/megacorp/employee/1/_update -d '
  {
    "script": "ctx._source.interest += new_interest",
    "params": {
       "new_interest": "food"
    }
  }'
  ```

## Retrieving a document
`GET /<index>/<type>/<id>`

Example:
```
curl http://localhost:9200/megacorp/employee/1?pretty
```

## Retrieving multiple documents
Example:
```
curl http://localhost:9200/_mget?pretty -d '
{
  "docs": [
    { "_index": "website", "_type": "blog", "_id": 2 },
    { "_index": "website", "_type": "blog", "_id": 3 }
  ]
}'
```

## Search
[Query DSL](https://goo.gl/OIxfxN)

Return all:  
`GET /<index>/<type>/_search`

Return all that match a value:  
  Using query string:  
  `GET /<index>/<type>/_search?q=field:<value>`

  Example:  
  ```
  curl 'http://localhost:9200/megacorp/employee/_search?q=last_name:Smith&pretty'
  ```

  Using request body:  
  ```
  GET /<index>/<type>/_search?q=field:<value>

  { "query": { <query values> } }
  ```

  Example:  
  ```
  curl http://localhost:9200/megacorp/employee/_search?pretty -d '
  {
      "query": {
          "match": {
              "last_name": "Smith"
          }
      }
  }'
  ```

Combine multiple clauses in a query:
  ```
  {
    "query": {
      "bool": {
        "must": [
          { "match": { "callSign": "FX" } },
          { "range": { "startDate": { "lte": "1496441530063" } } },
          { "range": { "endDate": { "gte": "1496441530063" } } }
        ]
      }
    }
  }
  ```

## Aggregations
Find the most popular interests of employees:
```
curl http://localhost:9200/megacorp/employee/_search?pretty -d '
{
  "aggs": {
    "all_interests": {
      "terms": { "field": "interests" }
    }
  }
}'
```

## Mapping / Schema definition
- Find the current schema definition for a type:
  `GET /<index>/_mapping/<type>`

  Example:
  ```
  curl http://localhost:9200/megacorp/_mapping/employee
  ```

## Batch processing (Scrolling)
[Reference](https://www.elastic.co/guide/en/elasticsearch/reference/1.6/search-request-scroll.html)

Example:
```
GET http://localhost:9200/foxvideo,fxvideo,ngcvideo/_search?scroll=1m
```

This will return a `_scroll_id`, which you can send in a `_search/scroll`
request to continue scrolling.

Pseudocode:
```
while(body.hits.hits.length > 0 && body['_scroll_id']) {
  request
  .post('http://localhost:9200/_search/scroll?scroll=1m')
  .send(scrollId)
}
```

## Other topics
- Word proximity
- Partial matching
- Relevance
- Stemming
- Stopwords
- Synonyms
- Fuzzy Matching
- Analytics
- Geolocation
- Efficient data modeling
