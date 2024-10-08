
### Makefile for a Spring Boot Project

```makefile
# Custom Makefile Name: CustomMakefile
# Variables
MVN = ./mvnw # Use Maven Wrapper, replace with mvn if not using
JAR_FILE = target/my-spring-boot-app.jar
APP_NAME = my-spring-boot-app
PROFILE = default # Change this to your desired Maven profile

# Default target
.PHONY: all
all: clean package

# Clean the project
.PHONY: clean
clean:
	@echo "Cleaning project..."
	$(MVN) clean

# Package the project (creates the JAR file)
.PHONY: package
package:
	@echo "Packaging the project..."
	$(MVN) package -P $(PROFILE) -DskipTests

# Run the Spring Boot application
.PHONY: run
run: all
	@echo "Running the Spring Boot application..."
	java -jar $(JAR_FILE)

# Run tests
.PHONY: test
test:
	@echo "Running tests..."
	$(MVN) test

# Build the JAR file with a specific profile
.PHONY: jar
jar: clean
	@echo "Creating executable JAR..."
	$(MVN) clean package -P $(PROFILE) -DskipTests

# Run the application with specific Java options
.PHONY: run-java-options
run-java-options: all
	@echo "Running the application with custom Java options..."
	java -Xmx512m -Dspring.profiles.active=dev -jar $(JAR_FILE)

# Build and run in a single step
.PHONY: build-and-run
build-and-run: all run

# Docker build and run (if using Docker)
.PHONY: docker
docker:
	@echo "Building Docker image..."
	docker build -t $(APP_NAME) .
	@echo "Running Docker container..."
	docker run -p 8080:8080 $(APP_NAME)

# Help target
.PHONY: help
help:
	@echo "Makefile Commands:"
	@echo "  make all              - Clean and package the project"
	@echo "  make clean            - Clean the project"
	@echo "  make package          - Package the project"
	@echo "  make run              - Run the Spring Boot application"
	@echo "  make test             - Run tests"
	@echo "  make jar              - Create executable JAR"
	@echo "  make run-java-options - Run with custom Java options"
	@echo "  make build-and-run    - Build and run in a single step"
	@echo "  make docker           - Build and run Docker image"
	@echo "  make help             - Show this help message"
```

### Breakdown of the Advanced Makefile:

1. **Custom Variables**:
   - `MVN`: Command to run Maven (use `./mvnw` for the Maven Wrapper).
   - `JAR_FILE`: Path to the JAR file generated by Maven.
   - `APP_NAME`: Name of the application, used for Docker.
   - `PROFILE`: Specify the Maven profile to use during packaging.

2. **Targets**:
   - **`all`**: Cleans and packages the project by default.
   - **`clean`**: Cleans the project using Maven.
   - **`package`**: Packages the project, skipping tests.
   - **`run`**: Runs the Spring Boot application.
   - **`test`**: Runs the unit tests using Maven.
   - **`jar`**: Creates the executable JAR file.
   - **`run-java-options`**: Runs the application with custom Java options (e.g., memory settings, active Spring profiles).
   - **`build-and-run`**: A convenient target to build the project and then run it immediately.
   - **`docker`**: Builds and runs a Docker image for the application (assuming you have a `Dockerfile`).
   - **`help`**: Provides a quick overview of available commands.

### How to Use the Advanced Makefile

1. **Clean and Package the Project**:
   ```bash
   make
   ```
   This runs the `all` target by default, cleaning and packaging the project.

2. **Run the Spring Boot Application**:
   ```bash
   make run
   ```

3. **Run Tests**:
   ```bash
   make test
   ```

4. **Create Executable JAR**:
   ```bash
   make jar
   ```

5. **Run with Custom Java Options**:
   ```bash
   make run-java-options
   ```

6. **Build and Run in a Single Step**:
   ```bash
   make build-and-run
   ```

7. **Build and Run Docker Image**:
   ```bash
   make docker
   ```

8. **Show Help**:
   ```bash
   make help
   ```

### Summary
This advanced Makefile for your Spring Boot project allows you to automate several aspects of the build process, from cleaning and packaging to running the application and tests. Additionally, it provides flexibility for custom Java options and Docker support.
