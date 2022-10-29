# The Docker ELK stack with Filebeat
The Docker ELK stack based on [deviantony/docker-elk repository](https://github.com/deviantony/docker-elk#elastic-stack-elk-on-docker), but changed to use filebeat with mysql slow query log.

The ELK stack is a log system consists of ElasticSearch+Logstash+Kibana.

To start up infrastructure use `docker compose up` command.
Password for root user for mysql you can find in the .env file. To test you are able to run `select sleep(5);` query.

Detailed setup information for the ELK stack you are to find in the deviantony/docker-elk repository.

### Problems that I faced
1. It possible that no such file or directory exists
Solution: create the file first
2. SET GLOBAL slow_query_log=ON	Error Code: 29. File '/var/log/mysql-slow.log' not found (OS errno 13 - Permission denied)
Solution: 
- chmod 666 mysql-slow.log
- +possible fix: sudo chown mysql:mysql /var/log/mysql
3. The custom cnf file wasn't uploaded. 
Solution: mount mysql.cnf file to /etc/mysql/conf.d/mysql.conf
4. After the start slow_query_log was set to OFF, I had to turn it manually
Solution: SET GLOBAL slow_query_log=ON;
