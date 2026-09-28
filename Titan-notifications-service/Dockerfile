FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

COPY target/titan-notifications-service-*.jar app.jar

EXPOSE 8084

HEALTHCHECK --interval=15s --timeout=5s --start-period=30s --retries=5 \
  CMD wget --no-verbose --tries=1 --spider http://localhost:8084/actuator/health || exit 1

ENTRYPOINT ["sh", "-c", "java ${JAVA_OPTS} -Dspring.profiles.active=${SPRING_PROFILES_ACTIVE:-docker} -jar app.jar"]
