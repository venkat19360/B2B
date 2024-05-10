# Use the official OpenJDK 17 JDK image with Alpine Linux as the base image
FROM openjdk:17-jdk-alpine as base

# Set the working directory in the container
WORKDIR /app

# Copy the JAR file from the host to the container and rename it to ecommerce.jar
COPY target/ecommerce-backend-0.0.1-SNAPSHOT.jar /app/ecommerce.jar

# Expose port 8081 (or whatever port your Spring Boot app listens on)
EXPOSE 8081

# Set the entry point for the container to run the Spring Boot application
ENTRYPOINT ["java", "-jar", "ecommerce.jar"]

# Use the base image to create a new image with the necessary dependencies
FROM base as final

# Remove unnecessary files and dependencies
RUN rm -rf /var/cache/apk/*

# Use specific versions for dependencies
RUN apk add --no-cache --virtual .build-deps \
    openjdk@17-jdk \
    && rm -rf /var/cache/apk/*

# Set the working directory in the final image
WORKDIR /app

# Copy the JAR file from the base image to the final image
COPY --from=base /app/ecommerce.jar /app/ecommerce.jar

# Expose port 8081 (or whatever port your Spring Boot app listens on)
EXPOSE 8081

# Set the entry point for the final image to run the Spring Boot application
ENTRYPOINT ["java", "-jar", "ecommerce.jar"]
