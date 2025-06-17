# Build stage
FROM openjdk:21 AS build
WORKDIR /app
COPY . .
# Grant execute permission and run the build for the BACKEND module
RUN chmod +x ./gradlew && ./gradlew :BACKEND:build -x test

# Run stage
FROM openjdk:21-jdk-slim
WORKDIR /app
COPY --from=build /app/BACKEND/build/libs/*.war drcomputer.war
EXPOSE 8080

ENTRYPOINT ["java","-jar","drcomputer.war"]