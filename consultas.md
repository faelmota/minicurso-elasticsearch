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

#Recupera o mapeamento de um index

```
GET /produtos/_mapping
```

#Listando os indices

```
GET /_cat/indices
```

#Exclui um indice

```
DELETE /produtos
```

#cria um index

```
PUT /produtos
{
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 0
  },
  "mappings": {
    "properties": {
      "codigo": {"type": "keyword"},
      "nome": {"type": "keyword"},
      "descricao": { "type": "text"},
      "categoria": {"type": "keyword"},
      "subcategoria": {"type": "keyword"},
      "preco": {"type": "float"},
      "estoque": {"type": "float"}
    }
  }
}
```

#Atualiza o mapeamento de um index

```
PUT /produtos/_mapping
{
  "properties": {
    "criado_em": { "type": "date"}
  }
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

#Atualiza documentos que correspondem à consulta especifica

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

#Exclui documentos que correspondem à consulta especifica

```
POST /produtos/_delete_by_query
{
  "query": {
    "match": {
      "codigo": "456ABC"
    }
  }
}
```

#Consulta um campo por um termo

```
GET /produtos/_search
{
  "query": {
    "term": {
      "categoria.keyword": "PERECIVEIS"
    }
  }
}
```

#pesquisa por um termo ignorando valores maiusculos ou minusculos

```
GET /produtos/_search
{
  "query": {
    "term": {
      "tags.keyword": {
        "value": "pereciveis",
        "case_insensitive": true
      }
    }
  }
}
```

#Pesquisa por produtos utilizando logica must

```
GET /produtos/_search
{
  "query": {
      "bool": {
        "must": [
          {
            "term": {
                "categoria.keyword": {
                    "value": "pereciveis",
                    "case_insensitive": true
                }
            }
        }, {
            "term": {
                "ativo": true
            }
        }]
    }
  }
}
```

#Pesquisa pelos termos contidos na lista

```
GET /produtos/_search
{
    "query": {
        "terms": {
            "categoria.keyword": ["LIMPEZA", "COSMETICOS"]
        }
    }
}

```

#pesquisa pelos termos que iniciam com o valor

```

GET /produtos/\_search
{
"query": {
"prefix": {
"descricao.keyword": {
"value": "sabao",
"case_insensitive": true
}
}
}
}

```

#Pesquisa utilizando wildcards
GET /produtos/\_search
{
"query": {
"wildcard": {
"descricao.keyword": {
"value": "leite\*",
"case_insensitive": true
}
}
}
}

#pesquisa por termos utilizando a logica or

```

GET /produtos/\_search
{
"query": {
"match": {
"descricao": "condensado lata"
}
}
}

```

#pesquisa por termos utilizando a logica and

```

GET /produtos/\_search
{
"query": {
"match": {
"descricao": {
"query": "lata condensado",
"operator": "and"
}
}
}
}

```

#pesquisa pelas valores que correspondem a frase obecendo a ordem da ocorrencia

```

GET /produtos/\_search
{
"query": {
"match_phrase": {
"descricao": "condensado leite"
}
}
}

```

#agrega os resultados por um campo

```

GET /produtos/\_search
{
"size": 0,
"aggs": {
"categoria": {
"terms": {
"field": "categoria.keyword"
},

      "aggs": {
        "preco_medio": {
          "avg": {
            "field": "preco"
          }
        },
        "qtde_estoque": {
          "sum": {
            "field": "qtde_estoque"
          }
        }
      }
    }

}
}

```

#ordena os resultados da consulta agregada
GET /produtos/\_search
{
"size": 0,
"aggs": {
"categoria": {
"terms": {
"field": "categoria.keyword"
},

      "aggs": {
        "preco_medio": {
          "avg": {
            "field": "preco"
          }
        },
        "qtde_estoque": {
          "sum": {
            "field": "qtde_estoque"
          }
        },
        "ordem_qtde_estoque": {
          "bucket_sort": {
            "sort": [{
              "qtde_estoque": "desc"
            }]
          }
        }
      }
    }

}
}

```

```
