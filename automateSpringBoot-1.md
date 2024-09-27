

### Example `Makefile` for Spring Boot

```makefile
# Variables
APP_NAME = my-spring-boot-app
JAR_FILE = target/$(APP_NAME).jar
MVN = ./mvnw # Use ./mvnw if using Maven Wrapper, otherwise just mvn

# Targets
.PHONY: clean compile package run

# Clean the project (removes the target directory)
clean:
	$(MVN) clean

# Compile the project (compiles and generates class files)
compile:
	$(MVN) compile

# Package the project (creates the JAR file)
package:
	$(MVN) package

# Run the Spring Boot application
run:
	$(MVN) spring-boot:run

# Build and run the application
build-run: package
	java -jar $(JAR_FILE)

# Shortcut for cleaning, building, and running the app
rebuild-run: clean package
	java -jar $(JAR_FILE)
```

### Breakdown of Commands:
1. **Variables**:
   - `APP_NAME`: Defines the name of the JAR file.
   - `JAR_FILE`: Defines where the JAR file will be generated.
   - `MVN`: Uses the Maven wrapper (`./mvnw`) or regular Maven (`mvn`) to run Maven commands.

2. **Targets**:
   - `clean`: Removes the `target` directory by running `mvn clean`.
   - `compile`: Compiles the project (`mvn compile`).
   - `package`: Packages the project into a JAR file (`mvn package`).
   - `run`: Runs the application using `mvn spring-boot:run`, which starts the Spring Boot application.
   - `build-run`: Packages the project into a JAR and then runs it using `java -jar`.
   - `rebuild-run`: Cleans the project, rebuilds the JAR, and then runs it.

### How to Use:
1. **Clean the project**:
   ```bash
   make clean
   ```

2. **Compile the project**:
   ```bash
   make compile
   ```

3. **Package the project into a JAR**:
   ```bash
   make package
   ```

4. **Run the Spring Boot application using Maven**:
   ```bash
   make run
   ```

5. **Build the JAR and run the application**:
   ```bash
   make build-run
   ```

6. **Clean, package, and run**:
   ```bash
   make rebuild-run
   ```

### Adding More Features:
- **Testing**: You could add a target to run tests using Maven (`mvn test`).
- **Docker Support**: If you're using Docker, you can add targets to build Docker images and run containers.
- **Profiling**: You could add commands for running the app with specific Spring profiles.

