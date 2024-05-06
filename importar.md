#Importa dados no elasticsearch
```
curl -k -u elastic -H "Content-type:application/x-ndjson" -XPOST http://localhost:9200/produtos/_bulk --data-binary "@produtos-bulk.json"
```