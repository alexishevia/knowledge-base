# To send JSON over curl
```sh
request_body() {
  NOW=$(node -e 'console.log(Date.now())')
  cat <<REQUEST_BODY
    {
      "query": {
        "range": {
          "startDate": { "gte": $NOW }
        }
      }
    }
REQUEST_BODY
}

request_body | curl -X POST \
  http://localhost:9200/epglistings/default/_search \
  -H 'Content-Type: application/json' \
  -d @- \
| jq
```
