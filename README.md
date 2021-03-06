# QGIS_SQL_Commands
## Comando para cálculo de estimativa de recepção em dBm usando os dados da ANATEL ([ANATEL2QGIS](https://github.com/mlbraga82/anatel2qgis))
<b>requisitos:</b>
- Colocar todas as camadas em um arquivo gpkg
- nome das camadas ("anatel" e "sensor")
- EPSG das camadas com sistema de coordenadas métricas (SIRGAS 2000 / UTM zone XXX)
```
select a.fid,round(st_distance(a.geom,b.geom)/1000,2) as dist_km,
a.TransmissaoInicial as freq,a.NomeEntidade as entidade, a.geom,a.PotenciaOperacao as pwr_tx_w,
round(10*log(a.PotenciaOperacao)+30-20*log(st_distance(a.geom,b.geom)/1000)-20*log(a.TransmissaoInicial)+32.44,2) as pwr_rx_dBm
 from "anatel" as a, "sensor" as b where freq = '880.0';	
 ```
 
 ## Referências
 1. [Friss Equation](https://en.wikipedia.org/wiki/Friis_transmission_equation)
 2. [Free Space Loss - Wikipedia](https://en.wikipedia.org/wiki/Free-space_path_loss)
