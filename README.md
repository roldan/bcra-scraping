# bcra-scraping

## Dependencias
- curl
- pup (requiere go)
- jq

#### CER (Base 2.2.2002=1)

```
curl 'http://www.bcra.gob.ar/PublicacionesEstadisticas/Principales_variables_datos.asp' \
	--data-raw 'fecha_desde=2002-02-02&fecha_hasta=2022-06-23&primeravez=1&serie=3540' \
| pup 'table.table-BCRA tbody tr json{}' | jq '.[].children | {"date": .[0].text, "value": .[1].text}'

...
{
  "date": "20/06/2022",
  "value": "50,3590"
}
{
  "date": "21/06/2022",
  "value": "50,4426"
}
{
  "date": "22/06/2022",
  "value": "50,5263"
}
{
  "date": "23/06/2022",
  "value": "50,6101"
}
```

#### BADLAR en pesos de bancos privados (en % n.a.)

```
curl 'http://www.bcra.gob.ar/PublicacionesEstadisticas/Principales_variables_datos.asp' \
	--data-raw 'fecha_desde=1999-01-04&fecha_hasta=2022-06-23&primeravez=1&serie=3540' \
| pup 'table.table-BCRA tbody tr json{}' | jq '.[].children | {"date": .[0].text, "value": .[1].text}'

...
{
  "date": "15/06/2022",
  "value": "46,5000"
}
{
  "date": "16/06/2022",
  "value": "46,6875"
}
{
  "date": "21/06/2022",
  "value": "50,8125"
}
```

#### Tipo de Cambio Mayorista ($ por US$) Comunicación A 3500 - Referencia

```
curl 'http://www.bcra.gob.ar/PublicacionesEstadisticas/Principales_variables_datos.asp' \
	--data-raw 'fecha_desde=2002-03-04&fecha_hasta=2022-06-23&primeravez=1&serie=272' \
| pup 'table.table-BCRA tbody tr json{}' | jq '.[].children | {"date": .[0].text, "value": .[1].text}'

...
{
  "date": "15/06/2022",
  "value": "122,69"
}
{
  "date": "16/06/2022",
  "value": "122,90"
}
{
  "date": "21/06/2022",
  "value": "123,69"
}
{
  "date": "22/06/2022",
  "value": "123,86"
}
```

