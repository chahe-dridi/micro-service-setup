FROM openjdk:17
EXPOSE 8093
ADD target/api-gateway-0.0.1-SNAPSHOT.jar api-gateway.jar
ENTRYPOINT ["java","-jar","api-gateway.jar"]