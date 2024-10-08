Here's a Makefile example saved with the **`.mak`** extension that automates various tasks for a Quarkus project. This Makefile includes targets for cleaning, building, running the application, and testing.

### Example `QuarkusProject.mak`

```makefile
# Quarkus Makefile: QuarkusProject.mak

# Variables
MVN = ./mvnw # Use Maven Wrapper, replace with mvn if not using
JAR_FILE = target/quarkus-app/quarkus-run.jar
APP_NAME = my-quarkus-app
PROFILE = dev # Change this to your desired Maven profile

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
	$(MVN) package -DskipTests

# Run the Quarkus application
.PHONY: run
run: all
	@echo "Running the Quarkus application..."
	java -jar $(JAR_FILE)

# Run tests
.PHONY: test
test:
	@echo "Running tests..."
	$(MVN) test

# Create a native executable (if using native mode)
.PHONY: native
native: clean
	@echo "Building native image..."
	$(MVN) package -Pnative -DskipTests

# Run the application in development mode
.PHONY: dev
dev:
	@echo "Starting Quarkus in dev mode..."
	$(MVN) quarkus:dev

# Help target
.PHONY: help
help:
	@echo "Makefile Commands:"
	@echo "  make all          - Clean and package the project"
	@echo "  make clean        - Clean the project"
	@echo "  make package      - Package the project"
	@echo "  make run          - Run the Quarkus application"
	@echo "  make test         - Run tests"
	@echo "  make native       - Create a native executable"
	@echo "  make dev          - Start Quarkus in development mode"
	@echo "  make help         - Show this help message"
```

### Breakdown of the Makefile:

1. **Variables**:
   - `MVN`: Command to run Maven (using the Maven Wrapper).
   - `JAR_FILE`: Path to the JAR file generated by Quarkus.
   - `APP_NAME`: Name of the application.
   - `PROFILE`: Specify the Maven profile to use during packaging.

2. **Targets**:
   - **`all`**: Cleans and packages the project by default.
   - **`clean`**: Cleans the project using Maven.
   - **`package`**: Packages the project, skipping tests.
   - **`run`**: Runs the Quarkus application using the generated JAR file.
   - **`test`**: Runs unit tests using Maven.
   - **`native`**: Builds a native image (if you are using native mode).
   - **`dev`**: Starts the Quarkus application in development mode, enabling hot reload.
   - **`help`**: Provides a quick overview of available commands.

### How to Use the `.mak` File

1. **Clean and Package the Project**:
   ```bash
   make -f QuarkusProject.mak
   ```

2. **Run the Quarkus Application**:
   ```bash
   make -f QuarkusProject.mak run
   ```

3. **Run Tests**:
   ```bash
   make -f QuarkusProject.mak test
   ```

4. **Create a Native Executable**:
   ```bash
   make -f QuarkusProject.mak native
   ```

5. **Run in Development Mode**:
   ```bash
   make -f QuarkusProject.mak dev
   ```

6. **Show Help**:
   ```bash
   make -f QuarkusProject.mak help
   ```

### Summary
This `.mak` file provides a convenient way to automate common tasks in your Quarkus project, allowing for efficient development and deployment. Feel free to adjust the targets and variables to suit your specific project requirements!
