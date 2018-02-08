dc exec ch-client clickhouse-client -h ch-server-1 --port=9001

cd examples
wget http://transtats.bts.gov/PREZIP/On_Time_On_Time_Performance_2017_1.zip
wget http://transtats.bts.gov/PREZIP/On_Time_On_Time_Performance_2017_2.zip
wget http://transtats.bts.gov/PREZIP/On_Time_On_Time_Performance_2017_3.zip

#unzip all

#dcu

dc exec ch-client clickhouse-client -h ch-server-1 --port=9001
dc exec ch-client clickhouse-client -h ch-server-2 --port=9002
dc exec ch-client clickhouse-client -h ch-server-3 --port=9003


cat examples/On_Time_On_Time_Performance_2017_1.csv | sed 's/\.00//g' | docker exec -i clickhouse_ch-client_1 /usr/bin/clickhouse-client --host ch-server-1 --port=9001 --query="INSERT INTO db.ontime_full FORMAT CSVWithNames"


select count(*) from db.ontime;
select count(*) from db.ontime_full;





=========
apt update
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
apt-add-repository "deb https://apt.dockerproject.org/repo ubuntu-xenial main"
apt update
apt install -y docker-engine
systemctl start docker
systemctl enable docker
usermod -aG docker ubuntu  # change ubuntu to username
# relogin
