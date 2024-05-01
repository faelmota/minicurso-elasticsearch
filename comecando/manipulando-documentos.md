#Adiciona um documento no indice
```
POST /produtos/_doc
{
  "nome": "Mesa de jantar",
  "descricao": "Mesa de jantar 4 cadeiras com tampo de vidro",
  "categoria": "Móveis",
  "subcategoria": "Mesas",
  "preco": 599.99,
  "estoque": 10
}
```

#Exclui um documento
```
DELETE /produtos/_doc/100
```

#Adiciona um documento com id
```
PUT /produtos/_doc/100
{
  "nome": "Mesa de jantar",
  "descricao": "Mesa de jantar 4 cadeiras com tampo de vidro",
  "categoria": "Móveis",
  "subcategoria": "Mesas",
  "preco": 599.99,
  "estoque": 10
}
```

#Atualiza campos no documento documento
```
POST /produtos/_update/100
{
    "doc": {
      "estoque": 99
    }
}
```

#Substitui um documento no index
```
PUT /produtos/_doc/100                  
{
  "nome": "Mesa de jantar",
  "descricao": "Mesa de jantar 4 cadeiras com tampo de vidro",
  "categoria": "Móveis",
  "subcategoria": "Mesas",
  "preco": 699.99,
  "estoque": 10
}
```

#Atualiza um documento com base em um filtro
```
POST /produtos/_update_by_query          
{
  "script": {
    "source": "ctx._source.categoria = 'MÓVEIS'",
    "lang": "painless"
  },
  "query": {
    "match": {
      "categoria": "Móveis"
    }
  }
}
```