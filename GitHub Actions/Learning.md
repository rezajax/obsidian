https://docs.github.com/en/actions


here is echo for summary
https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions


a simple summary
```yml
name: Kotlin Build and Test  
  
on:  
  push:  
    branches:  
      - master  
  pull_request:  
    branches:  
      - master  
  workflow_dispatch:  
  
  
jobs:  
  build:  
    runs-on: ubuntu-latest  
      
    steps:  
      - name: Check out repository  
        uses: actions/checkout@v4  
  
      - name: Set up JDK 21  
        uses: actions/setup-java@v4  
        with:  
          distribution: 'temurin'  
          java-version: '21'  
  
      - name: Build with Gradle  
        run: ./gradlew build  
  
      - name: Run tests  
        run: ./gradlew test  
  
      - name: install cowsay  
        run: sudo apt-get install cowsay  
  
      - name: Build with Gradle and publish build scan  
        run: |  
          ./gradlew build --scan  
          echo "## Reza Title من رضا هستم" >> $GITHUB_STEP_SUMMARY  
          echo "JDK Version:" >> $GITHUB_STEP_SUMMARY  
          java -version >> $GITHUB_STEP_SUMMARY  
          cowsay "سلام رضا" >> $GITHUB_STEP_SUMMARY  
            
            
            
  
      - name: Run cowsay  
        run: cowsay "Hello World"
```


a simple with gradle plugin
https://github.com/gradle/gradle-build-action
https://github.com/marketplace/actions/build-with-gradle

```yml
name: Build  
  
on: [ push ]  
  
jobs:  
  build:  
    runs-on: ubuntu-latest  
    steps:  
      - name: Checkout sources  
        uses: actions/checkout@v4  
  
      - name: Setup Gradle  
        uses: gradle/actions/setup-gradle@v3.5.0  
  
      - name: Print JDK version  
        run: |  
          echo "JDK Version:"  
          java -version  
  
      - name: Build with Gradle and publish build scan  
        run: |  
          ./gradlew build --scan  
          echo "## Reza Title" >> $GITHUB_STEP_SUMMARY  
          echo "JDK Version:" >> $GITHUB_STEP_SUMMARY  
          java -version >> $GITHUB_STEP_SUMMARY
```

