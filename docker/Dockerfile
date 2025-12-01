# Use Temurin 17 JDK as a base image (stable, maintained)
FROM eclipse-temurin:17-jdk-jammy

WORKDIR /app
COPY target/student-management-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8089
ENTRYPOINT ["java","-jar","app.jar"]
