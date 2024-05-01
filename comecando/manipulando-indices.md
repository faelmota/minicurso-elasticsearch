#Listando os indices

```
GET /_cat/indices
```

#Criando um indice

```
PUT /nome-do-index
{
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 0
  }
}
```

#Exclui um indice
```
DELETE /nome-do-index
```