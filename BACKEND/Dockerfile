# Build stage
FROM openjdk:21 AS build
WORKDIR /app
COPY . .  # Sao chép toàn bộ vào Docker context
WORKDIR /app/BACKEND  # Chuyển vào thư mục BACKEND
RUN chmod +x ./gradlew && ./gradlew build -x test

# Run stage
FROM openjdk:21-jdk-slim
WORKDIR /app
COPY --from=build /app/BACKEND/build/libs/*.war drcomputer.war
EXPOSE 8080

ENTRYPOINT ["java", "-jar", "drcomputer.war"]
