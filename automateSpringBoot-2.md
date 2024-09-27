

### Makefile with a Single Command (`all`)

```makefile
# Variables
APP_NAME = my-spring-boot-app
JAR_FILE = target/$(APP_NAME).jar
MVN = ./mvnw # Use ./mvnw if using Maven Wrapper, otherwise just mvn

# Targets
.PHONY: all clean compile package run

# Run all tasks with a single command
all: clean package run-jar

# Clean the project (removes the target directory)
clean:
	$(MVN) clean

# Compile the project (optional but can be added before package)
compile:
	$(MVN) compile

# Package the project (creates the JAR file)
package:
	$(MVN) package

# Run the JAR file
run-jar:
	java -jar $(JAR_FILE)
```

### Explanation:
- The target `all` is defined as a combination of `clean`, `package`, and `run-jar`.
- When you run `make all` or just `make`, it will automatically:
  1. **Clean** the project.
  2. **Package** the project into a JAR.
  3. **Run** the JAR file.

### How to Use:

1. Run the following single command to automate everything:
   ```bash
   make
   ```
   - This will clean the project, compile and package it, and run the application.
