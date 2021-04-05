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
 
 ## Motivace
 
 Na týmovém projektu může mít každý vývojář nastavené prostředí podle sebe. Často se také nastavení prostředí musí měnit během projektu a návod vytvořený na začátku projektu nemusí být aktuální. Nejlepší je se takovým problémům vyvarovat a vytvořit skript na automatický build a testování celého projektu a tento skript automaticky spoštět po každé změně. Tím se zajistí, že každý uvidí aktuální stav.
 
 ## Terminologie CI/CD
 
 Existuje několik různých definic zkratky CI/CD, které mají určitý překryv svého významu.
 
 `Continuous Integration` - 
 `Continuous Development` - 
 `Continuous Deployment` - 
 `Continuous Delivery` - 
 
 ## Seznámení s GitHub Actions
  
 ### Trigger (on)
 
 V první části nastavíme možnosti, kdy se daný skript spouští. Možností je několik:
 - push - V momentě, kdy je do repozitáře pushnutý nový kód
 - pull_request - V momentě, kdy je vytvořený nový pull request
 - workflow_dispatch - Možnost manuálně spustit workflow z Webového rozhraní GitHubu
 
 on: [push, pull_request, workflow_dispatch]
 
 ### Akce (jobs)
 
 Zde definujeme hlavní blok skriptu. Definujeme jednotlivé bloky a také typ docker image, na kterém se skript spustí.
 
 ### Kroky (steps)
 
 V této části definujeme jednotlivé kroky pro build, spustění testů. U každého kroku se dají nastavit parametry.
 
 ## Ukázkový skript

Vytvořte soubor: `.github\workflows\ci.yaml`

Pozor, je potreba upravit prava na souboru `mvnw`: `git update-index --chmod=+x mvnw`

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
