# build gradle
FROM gradle:jdk17 AS build
COPY --chown=gradle:gradle ./settings.gradle /home/gradle/src/settings.gradle
COPY --chown=gradle:gradle build.gradle /home/gradle/src/
COPY --chown=gradle:gradle . /home/gradle/src/api
WORKDIR /home/gradle/src
RUN gradle build -x test --stacktrace

# production deployment
FROM openjdk:17-jdk-slim
ENV EXPOSE_PORT=8080

EXPOSE ${EXPOSE_PORT}

RUN mkdir /app
COPY --from=build ./build/libs/*.jar /app/api.jar
CMD ["java", "-XshowSettings:vm", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseContainerSupport", "-jar", "/app/api.jar""--spring.config.location=classpath:/${MODE}.properties"]
