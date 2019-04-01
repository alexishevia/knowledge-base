## Installing mongodb using Docker

docker-compose.yml
```
version: "3"

volumes:
  mongouniversity:

services:
  mongo:
    build:
      context: .
    volumes:
      - mongouniversity:/data/db
    ports:
      - "27017:27017"
```

Dockerfile
```
FROM mongo:3.2

COPY mongod.conf /etc/mongod.conf
```

# GUI
[Robomongo](https://robomongo.org/)

## Mongo Shell

Start shell: `mongo`

Show available commands: `help`

Mongo-shell cheatsheet: https://docs.mongodb.com/manual/reference/mongo-shell/

```
show dbs
use <db>
show collections
```

## Restore mongo from a binary dump directory
When you restore mongo from a binary dump directory, every subdirectory will
turn into a db, and each file in the subdirectory will convert into a
collection.
```
mongorestore <path/to/dump/directory>
```

## Restore mongo from a JSON file
```
mongoimport -d yourdb -c yourcollection somefile.json
```

## Indexes
There are several types of indexes:
- Regular
- Sparse (doesn't include documents where the value for the index key is null)
- Multikey (index on an array field)
- 2d (for [x,y] attributes)
- 2dsphere (for geographical attributes)
- text (for full-text search)

create regular index:
```
db.collectionName.createIndex({field: 1}); // 1 ascending, -1 descending
```

create sparse index:
```
db.collectionName.createIndex({field: 1}, {sparse: false});
```

create 2d index:
Note: you can call your 2d field any name you want, but it must be
an array having x and y values, eg: [5,20]
```
db.collectionName.createIndex({some2dField: '2d'});
```

use 2d index:
```
db.collectionName.find({some2dField: {$near: [50, -75]}}).limit(10);
```

create 2dsphere index:
Note: you can call your geo field any name you want, but it must be either a
Point or Polygon, specified following the [GeoJSON format](http://geojson.org/)
```
db.collectionName.createIndex({someGeoField: '2dsphere'});
```

use 2dsphere index:
```
db.collectionName.find({someGeoField: {
  $near: {
    $geometry: {
      type: "Point",
      coordinates: [-122.166641, 37.4278925] // lon,lat
    },
    $maxDistance: 2000 // meters
  }
}}).limit(10);
```

create text index:
```
db.collectionName.createIndex({someTextField: 'text'})
db.collectionName.createIndex({someTextField: 'text', otherTextField: 'text'})
```

use text index:
```
db.collectionName.find({$text:{$search:'foo'}})
```

list all indexes:
```
db.collectionName.getIndexes();
```

drop index:
Note: you need to use the same attributes you used when creating the index
```
db.collectionName.dropIndex({field: 1});
```

## Explain query

db.collectionName.explain().yourQuery

example:
```
db.books.explain().find({author: 'Mark Twain'});
```

## Storage Engines
Mongo now supports 2 storage engines:
- MMAP: the traditional storage engine
- WiredTiger:
  * supports document-level locking instead of collection-level locking
  * supports data compression

## Aggregation Pipeline

db.collectionName.aggregate([
  {stage1}, {stage2}, ...
])

aggregation pipeline stages:
https://docs.mongodb.com/manual/reference/operator/aggregation-pipeline/
- $match
- $limit
- $project
- $sort
- $unwind
etc

example aggregation:
```
db.companies.aggregate( [
    { $match: { "relationships.person": { $ne: null } } },
    { $project: { relationships: 1, _id: 0 } },
    { $unwind: "$relationships" },
    { $group: {
        _id: "$relationships.person",
        count: { $sum: 1 }
    } },
    { $sort: { count: -1 } }
] )
```
