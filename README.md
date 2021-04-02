<p align="center">
  <img src="https://engeto.cz/wp-content/uploads/2019/01/engeto-square.png" width="200" height="200">
</p>

# GitHub Actions

V dněšní hodině si projdeme úvod do CI/CD a ukážeme si nástroj GitHub Actions, který je zdarma k dispozici k účtu na GitHubu.

## Co bychom měli mít hotové

V předchozích lekcích jsme se seznámili s nástrojem Maven (případně Gradle) na buildování aplikace a ukázali jsme si, jak testovat aplikaci pomocí JUnit testů.

## Co nás čeká

 - [Motivace](#motivace)
 - [Terminologie CI/CD](#terminologie-cicd)
 - [Seznámení s GitHub Actions](#seznámení-s-github-actions) 
 - [Ukázkový skript](#ukázkový-skript)
 -  
 ## Motivace
 
 ## Terminologie CI/CD
 
 ## Seznámení s GitHub Actions
 
 ## Ukázkový skript

Vytvořte soubor: `.github\workflows\ci.yaml`

```
name: Java CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up JDK 11
        uses: actions/setup-java@v1
        with:
          java-version: 11
      - name: Build with Maven
        run: ./mvnw clean install
      - name: Archive production artifacts
        if: always()
        uses: actions/upload-artifact@v2        
        with:
          name: dist-without-markdown
          path: |
            target/surefire-report
```
