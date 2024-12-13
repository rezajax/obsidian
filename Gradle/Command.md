
To create a Gradle wrapper for your project, you can use the following command from your project directory:

```bash
gradle wrapper
```
This will generate the wrapper files in your project directory, typically:

- `gradlew` (a script for Unix-based systems)
- `gradlew.bat` (a script for Windows systems)
- A `gradle/wrapper` directory containing `gradle-wrapper.properties` and `gradle-wrapper.jar`.

### Customize the Wrapper Version

If you want to specify a particular Gradle version, use the `--gradle-version` option:

bash

Copy code

`gradle wrapper --gradle-version <version>`

For example:

bash

Copy code

`gradle wrapper --gradle-version 8.3`

This ensures your project uses the specified Gradle version, making it easier to maintain consistency across environments. After running the command, you'll find the updated wrapper files in your project directory.