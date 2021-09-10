# QGIS_SQL_Commands

select a.fid,round(st_distance(a.geom,b.geom)/1000,2) as dist_km,
a.TransmissaoInicial as freq,a.NomeEntidade as entidade, a.geom,a.PotenciaOperacao as pwr_tx_w,
round(10*log(a.PotenciaOperacao)+30-20*log(st_distance(a.geom,b.geom)/1000)-20*log(a.TransmissaoInicial)+32.44,2) as pwr_rx_dBm
 from "anatel" as a, "sensor" as b where freq = '880.0';	
 
