FROM openjdk:11-alpine
ENTRYPOINT ["/usr/bin/${{values.artifact_id}}.sh"]

COPY ${{values.artifact_id}}.sh /usr/bin/${{values.artifact_id}}.sh
COPY target/${{values.artifact_id}}.jar /usr/share/${{values.artifact_id}}/${{values.artifact_id}}.jar



FROM maven:3.8.1-jdk-11-slim AS build

WORKDIR /opt/app

COPY ./src src
COPY pom.xml .

RUN mvn -f pom.xml clean install -DskipTests

FROM azul/zulu-openjdk-alpine:11

COPY --from=build /opt/app/target/${{values.artifact_id}}*.jar ${{values.artifact_id}}.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "${{values.artifact_id}}.jar"]
