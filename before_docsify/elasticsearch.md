# Elasticsearch

## Installing elasticsearch in Ubuntu

- [Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html)
- [Kibana](https://www.elastic.co/guide/en/kibana/current/deb.html)
- [X-Pack](https://www.elastic.co/guide/en/x-pack/current/installing-xpack.html#xpack-package-installation)

Start elasticsearch
```
sudo service elasticsearch start
sudo service kibana start
```

Open
- Elasticsearch: http://localhost:9200
- Kibana: http://localhost:5601

## Installing elasticsearch using Docker

docker-compose.yml
```
version: "3"

volumes:
  myvolume:

services:
  es:
    build:
      context: ./elasticsearch
    volumes:
      - myvolume:/usr/share/elasticsearch/data
    ports:
      - "9200:9200"
```

Dockerfile
```
FROM elasticsearch:1.6
```

## Elastic Stack

- Ingest:  
  Logstash, Beats

- Store, Index, Analyze:  
  Elasticsearch

- User Interface:  
  Kibana  
  [Getting Started with Kibana](https://www.elastic.co/webinars/getting-started-kibana)

- Plugins / Extended Features:  
  X-Pack (security, alerting, monitoring, graph, reporting)


## Concepts
In Elasticsearch, a `document` belongs to a `type`, and those types live inside
an `index`.

```
Relational DB ⇒ Databases ⇒ Tables ⇒ Rows      ⇒ Columns
Elasticsearch ⇒ Indices   ⇒ Types  ⇒ Documents ⇒ Fields
```
