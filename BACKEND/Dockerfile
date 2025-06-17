# Build stage
FROM openjdk:21 AS build
WORKDIR /app

# Copy the Gradle wrapper
COPY gradlew .
COPY gradlew.bat .
COPY gradle/wrapper/gradle-wrapper.jar .

# Copy build configuration
COPY build.gradle .
COPY settings.gradle .

# Copy source code
COPY src/ src/

# Grant execute permission and run the build
RUN chmod +x gradlew && ./gradlew build -x test

# Run stage
FROM openjdk:21-jdk-slim
WORKDIR /app
COPY --from=build /app/build/libs/*.war drcomputer.war
EXPOSE 8080

ENTRYPOINT ["java","-jar","drcomputer.war"]
