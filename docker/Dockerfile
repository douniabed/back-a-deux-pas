# Production image using pre-built JAR from CI pipeline
FROM eclipse-temurin:21-jre

ARG APP_NAME=back-a-deux-pas
ARG APP_VERSION=2.0.0-SNAPSHOT
ARG APP_UID=1001
ARG SPRING_PROFILES_ACTIVE=docker

# Create app user to avoid running app as root
RUN useradd -U -m -d /app/ -s /bin/bash -u ${APP_UID} app-user

WORKDIR /app

# Copy pre-built JAR from CI pipeline
COPY --chown=${APP_UID}:${APP_UID} ./target/${APP_NAME}-${APP_VERSION}.jar /app/app.jar

USER app-user

# Expose application port
EXPOSE 8081

# Run with configurable Spring profile via environment variable
ENV SPRING_PROFILES_ACTIVE=${SPRING_PROFILES_ACTIVE}
CMD ["java", "-jar", "/app/app.jar"]
