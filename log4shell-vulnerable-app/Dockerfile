FROM gradle:7.3.1-jdk17-alpine AS builder
COPY --chown=gradle:gradle ./log4shell-vulnerable-app/ /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle bootJar --no-daemon


FROM openjdk:8u181-jdk-alpine
EXPOSE 8080
RUN mkdir /app
COPY --from=builder /home/gradle/src/build/libs/*.jar /app/spring-boot-application.jar
ADD ../twistlock_defender_app_embedded.tar.gz /
ENV DEFENDER_TYPE="appEmbedded"
ENV DEFENDER_APP_ID="cloudrun-vuln-app"
ENV FILESYSTEM_MONITORING="true"
ENV WS_ADDRESS="wss://us-east1.cloud.twistlock.com:443"
ENV DATA_FOLDER="/app"
ENV INSTALL_BUNDLE="eyJzZWNyZXRzIjp7InNlcnZpY2UtcGFyYW1ldGVyIjoiYjFVd2RpeUJKeUhqaGdiQjNrNGMvRTF4ejhIR3VMcExnNG9WTTNSc3pKcldMYzVMM1pTb0FlN2N0bEJjeEQzL2RhclJaclFjOHQ0Mlh5SkQ1WlVrS1E9PSJ9LCJnbG9iYWxQcm94eU9wdCI6eyJodHRwUHJveHkiOiIiLCJub1Byb3h5IjoiIiwiY2EiOiIiLCJ1c2VyIjoiIiwicGFzc3dvcmQiOnsiZW5jcnlwdGVkIjoiIn19LCJjdXN0b21lcklEIjoidXMtMi0xNTgyNTY4ODUiLCJhcGlLZXkiOiI5YlloWFMvTzIyKzhqNDQxTHFHcENCR1dvRlVtK3dzdHlZWjFvNnpEV29kV2dYa01JQXRiUUV3eDl6TmZYWEJNb1pRd1htYWszNXpyY1hCWkdMQ290dz09IiwibWljcm9zZWdDb21wYXRpYmxlIjpmYWxzZSwiaW1hZ2VTY2FuSUQiOiJhNDcwODhmYS02Y2EwLTJjMmMtOWM3NC0xYjViZWMzYzczOTUifQ=="
CMD ["/defender app-embedded", "java", "-jar", "/app/spring-boot-application.jar"]


