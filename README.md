
name: Build Android APK

on:
  workflow_dispatch:
  push:
    branches: [main, master]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Get project files
        uses: actions/checkout@v4

      - name: Install Java
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - name: Build debug APK
        run: gradle assembleDebug

      - name: Save APK
        uses: actions/upload-artifact@v4
        with:
          name: Stylish-Enterprises-APK
          path: app/build/outputs/apk/debug/*.apk
          if-no-files-found: error

        
