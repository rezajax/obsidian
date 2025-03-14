```yml
name: publishJar

on:
  push:
    branches:
      - master
  workflow_dispatch:


jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up JDK 21
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '21'

      - name: Build JAR
        run: ./gradlew clean shadowJar

      - name: Upload JAR artifact
        uses: actions/upload-artifact@v4
        with:
          name: app-jar
          path: build/libs/my-shadow-jar-1.0.0-all.jar # مسیر دقیق فایل JAR

  release:
    needs: build
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Download JAR artifact
        uses: actions/download-artifact@v4
        with:
          name: app-jar

      - name: Generate tag
        id: generate_tag
        run: echo "::set-output name=tag::v$(date +'%Y%m%d-%H%M%S')"

      - name: Create GitHub Release
        uses: ncipollo/release-action@v1.14.0
        with:
          artifacts: my-shadow-jar-1.0.0-all.jar # اشاره به فایل JAR دانلود شده
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
          cowsay "release is done: ${{ steps.generate_tag.outputs.tag }}" >> $GITHUB_STEP_SUMMARY
```