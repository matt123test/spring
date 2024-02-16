# spring boot app that connects to elasticache redis
Sample springboot app to connect to elasticache redis

Environment:
------------
OS: Amazon Linux 2

Packages:
maven
jdk17

Redis:
Multi-AZ: Disabled
Cluster Mode Enabled cluster 
Engine: 7.1.0
In-Transit Encryption:	Not Enabled
At-Rest Encryption:	Enabled

Steps:
-----
> wget https://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
> sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
> sudo yum install -y apache-maven -y
> sudo yum install java-17-amazon-corretto-headless -y 
> sudo alternatives --config java


Contents:
--------
- Provide the cluster name for the parameter "spring.redis.cluster.nodes" in the file "springboot-data-cme-lab/src/main/resources/application.properties"
spring.redis.cluster.nodes=clustercfg.cache.amazonaws.com:6379

Testing:
--------
- Compile and build : 
> mvn spring-boot:run

- Set up a key using command in a parallel terminal: 
> curl -s --location --request POST 'http://localhost:8080/api/key' --header 'Content-Type: application/json' --data-raw '{ "mykey1": "myvalue" }'

- Once the key was set I tried accessing it using : 
> curl --location --request GET 'http://localhost:8080/api/key/mykey1'
