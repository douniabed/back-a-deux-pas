# Production image using pre-built JAR from CI pipeline
FROM eclipse-temurin:21-jre

ARG APP_NAME=back-a-deux-pas \
    APP_VERSION=2.0.0-SNAPSHOT \
    APP_UID=1001

# Create app user to avoid running app as root
RUN useradd -U -m -d /app/ -s /bin/bash -u ${APP_UID} app-user

USER app-user
WORKDIR /app

# Copy pre-built JAR from CI pipeline
COPY --chown=${APP_UID}:${APP_UID} ./target/${APP_NAME}-${APP_VERSION}.jar /app/back-a-deux-pas.jar

# set default command to start application and expose application port
CMD ["sh", "-c", "java -Dspring.profiles.active=docker -jar /app/back-a-deux-pas.jar"]
EXPOSE 8081
