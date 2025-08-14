# Use OpenJDK 21 as the base image
FROM openjdk:21-jdk-slim

# Set the working directory
WORKDIR /app

# Copy Maven wrapper and pom.xml first for better caching
COPY .mvn/ .mvn/
COPY mvnw pom.xml ./

# Download dependencies
RUN ./mvnw dependency:go-offline

# Copy source code
COPY src ./src

# Build the application
RUN ./mvnw package -DskipTests

# Run the jar file
CMD ["java", "-jar", "target/eureka-server-0.0.1-SNAPSHOT.jar"]
