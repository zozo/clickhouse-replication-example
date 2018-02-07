dc exec ch-client clickhouse-client -h ch-server-1

cd examples
wget http://transtats.bts.gov/PREZIP/On_Time_On_Time_Performance_2017_1.zip
wget http://transtats.bts.gov/PREZIP/On_Time_On_Time_Performance_2017_2.zip
wget http://transtats.bts.gov/PREZIP/On_Time_On_Time_Performance_2017_3.zip

#unzip all

#dcu

dc exec ch-client clickhouse-client -h ch-server-1
dc exec ch-client clickhouse-client -h ch-server-2
dc exec ch-client clickhouse-client -h ch-server-3


cat examples/On_Time_On_Time_Performance_2017_1.csv | sed 's/\.00//g' | docker exec -i clickhouse_ch-client_1 /usr/bin/clickhouse-client --host ch-server-1 --query="INSERT INTO ontime FORMAT CSVWithNames"
cat examples/On_Time_On_Time_Performance_2017_2.csv | sed 's/\.00//g' | docker exec -i clickhouse_ch-client_1 /usr/bin/clickhouse-client --host ch-server-2 --query="INSERT INTO ontime FORMAT CSVWithNames"
cat examples/On_Time_On_Time_Performance_2017_3.csv | sed 's/\.00//g' | docker exec -i clickhouse_ch-client_1 /usr/bin/clickhouse-client --host ch-server-3 --query="INSERT INTO ontime FORMAT CSVWithNames"



select count(*) from default.ontime;
select count(*) from r0.ontime;
select count(*) from r1.ontime;

select count(*) from default.ontime;
select count(*) from default.ontime;
