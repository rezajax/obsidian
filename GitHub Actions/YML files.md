
# First
```yml
name: Build and Release JAR

on:
  push:
    branches:
      - master # اجرا برای هر push روی شاخه main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # Checkout repository
      - name: Checkout code
        uses: actions/checkout@v3

      # Set up JDK
      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '17'

      # Build the JAR
      - name: Build JAR
        run: ./gradlew clean build

      # Upload the JAR as an artifact
      - name: Upload JAR artifact
        uses: actions/upload-artifact@v3
        with:
          name: app-jar
          path: build/libs/*.jar

  release:
    needs: build
    runs-on: ubuntu-latest

    steps:
      # Checkout repository
      - name: Checkout code
        uses: actions/checkout@v3

      # Download the built JAR artifact
      - name: Download JAR artifact
        uses: actions/download-artifact@v3
        with:
          name: app-jar

      # Generate a timestamp-based tag
      - name: Generate tag
        id: generate_tag
        run: echo "::set-output name=tag::v$(date +'%Y%m%d-%H%M%S')"

      # Publish Release
      - name: Create GitHub Release
        uses: ncipollo/release-action@v1
        with:
          artifacts: app-jar
          token: ${{ secrets.GITHUB_TOKEN }}
          tag: ${{ steps.generate_tag.outputs.tag }} # استفاده از تگ بر اساس زمان
          name: "Release ${{ steps.generate_tag.outputs.tag }}"
          body: |
            This release contains the latest build of the project.
            Download the JAR file below.
          draft: false
          prerelease: false

```


# Second
```yml
name: Build and Release JAR2

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Build JAR
        run: ./gradlew clean build

      - name: Upload JAR artifact
        uses: actions/upload-artifact@v3
        with:
          name: app-jar
          path: build/libs/exposd-all.jar # مسیر دقیق فایل JAR

  release:
    needs: build
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Download JAR artifact
        uses: actions/download-artifact@v3
        with:
          name: app-jar

      - name: Generate tag
        id: generate_tag
        run: echo "::set-output name=tag::v$(date +'%Y%m%d-%H%M%S')"

      - name: Create GitHub Release
        uses: ncipollo/release-action@v1
        with:
          artifacts: exposd-all.jar # اشاره به فایل JAR دانلود شده
          token: ${{ secrets.GITHUB_TOKEN }}
          tag: ${{ steps.generate_tag.outputs.tag }}
          name: "Release ${{ steps.generate_tag.outputs.tag }}"
          body: |
            This release contains the latest build of the project.
            Download the JAR file below.
          draft: false
          prerelease: false

      - name: install cowsay
        run: |
          sudo apt-get update
          sudo apt-get install -y cowsay
          cowsay "release is done: ${{ steps.generate_tag.outputs.tag }}"

      - name: save release info
        run: |
          echo "release is done: ${{ steps.generate_tag.outputs.tag }}" >> $GITHUB_STEP_SUMMARY

```

