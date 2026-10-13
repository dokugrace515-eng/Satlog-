# Satlog-
Satlog betting 
name: Build Satlog APK

on:
  workflow_dispatch:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Get Satlog source
        uses: actions/checkout@v4

      - name: Set up Java 17
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: "17"

      - name: Set up Gradle
        uses: gradle/actions/setup-gradle@v4

      - name: Allow Gradle to run
        run: chmod +x gradlew

      - name: Build Satlog APK
        run: ./gradlew assembleDebug

      - name: Upload Satlog APK
        uses: actions/upload-artifact@v4
        with:
          name: Satlog-APK
          path: app/build/outputs/apk/debug/*.apk
          if-no-files-found: error
