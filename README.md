# elk-deploy
The Elastic stack (ELK) deploy by Docker and Compose.

## docker
版本：7.17.8
```shell
# 网络
docker network create elastic

# elasticsearch,ES_JAVA_OPTS指定内存，否则会提示内存不足；
docker run -d --name es01-test --net elastic -p 127.0.0.1:9200:9200 -p 127.0.0.1:9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms512m -Xmx512m"  docker.elastic.co/elasticsearch/elasticsearch:7.17.8

# logstash,配置地址：/Users/bob/docker/logstash
docker run -d  --name logstash --net elastic -p 5001:5001 -v /Users/bob/docker/logstash/pipeline:/usr/share/logstash/pipeline -v /Users/bob/docker/logstash/config:/usr/share/logstash/config docker.elastic.co/logstash/logstash:7.17.8
# kibana
docker run -d --name kib01-test --net elastic -p 127.0.0.1:5601:5601 -e "ELASTICSEARCH_HOSTS=http://es01-test:9200" docker.elastic.co/kibana/kibana:7.17.8
```
 参考
[Install Elasticsearch with Docker | Elasticsearch Guide [7.17] | Elastic](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/docker.html)
[Create an index pattern | Kibana Guide [7.17] | Elastic](https://www.elastic.co/guide/en/kibana/7.17/index-patterns.html)

