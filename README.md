# run application standalone
mvn clean install spring-boot:run

# run postgres sql with docker
docker run --name spring-boot-jpa-postgres -p 5444:5432 -e POSTGRES_PASSWORD=1q2w3e4r -d postgres
docker logs spring-boot-jpa-postgres -f

# Test link
http://localhost:8080/spring-boot-jpa-postgres/api/notes

# run application with docker-compose
mvn clean install -DskipTests
docker-compose up -d --build

# Test link
http://192.168.99.100:8082/spring-boot-jpa-postgres/api/notes

# kubernetes
mvn clean install -DskipTests
eval $(minikube docker-env)
docker build -t="spring-boot-rest-jpa:v1.0" .
kubectl create -f deployment-datasource.yml
kubectl create -f deployment-rest-api.yml

# Test link
http://192.168.99.101:8080/spring-boot-jpa-postgres/api/notes