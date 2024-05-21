---
date: 2024-05-21 19:20:39
layout: post
title: Adventure Time Quote Generator
subtitle: A simple clean architecture mobile application built with flutter
description: A simple application that generates a quote using a third party
  API, built for the sole purpose of testing Clean Architecture in a flutter
  project.
image: /assets/img/uploads/at3.jpeg
category: portfolio
tags:
  - Flutter
  - Dart
  - Clean-Architecture
author: Dan
paginate: false
---
# Tech Used

* Flutter
* Dart
* Third-Party API

# Project Details

A﻿dventure Time Quote Generator is a simple application that generates a quote using a third party API.
I﻿t was built for the sole purpose of testing Clean Architecture in a Flutter project.

C﻿heck the code out on [GitHub](https://github.com/DanArcherOnline/Adventure_Time_Quote_Generator).

![Application in initial state](/assets/img/uploads/at1.png "Application in initial state")

![Application in quote generated state](/assets/img/uploads/at2.png "Application in quote generated state")



B﻿elow is a Mermaid chart showing the Clean Architecture of the app and the relationships between the different layers.

```mermaid
    C4Component
    title Component diagram for Adventure Time Quote Generator

    Container_Boundary(pr, "Presentation") {
        Container(widgets, "Widgets", "UI in Flutter and Dart")
        Container(vm, "ViewModel", "BLoC Flutter Statemanagement")

        Rel(vm, widgets, "Updates the state of the application")
        UpdateRelStyle(vm, widgets, $textColor="lightblue", $offsetY="40", $offsetX="-100")
        Rel(widgets, vm, "Listens for changes to the state of the application")
        UpdateRelStyle(widgets, vm, $textColor="lightblue", $offsetY="-70", $offsetX="-100")
    }

    Rel(uc, vm, "Updates the state of <br> the application based on <br> the result of the business logic")
    UpdateRelStyle(uc, vm, $textColor="lightblue" $offsetY="40", $offsetX="-70")

    Container_Boundary(do, "Domain") {
        Component(uc, "Use Cases", "Business logic in Dart")
        Component(ent, "Entities", "Domain-based objects")

        Rel(ent, uc, "entities are managed and used by use cases")
        UpdateRelStyle(ent, uc, $textColor="lightblue", $offsetX="-100")
    }

    Rel(repo, ent, "The repositories create entities from external data")
    UpdateRelStyle(repo, ent, $textColor="lightblue" $offsetY="0", $offsetX="-100")
    
    
    Container_Boundary(da, "Data") {
        Component(repo, "Repositories", "Repository Pattern")
        Component(m, "Models", "Application Data DTO",)
        Component(rds, "Remote Data Sources", "Remote Data Logic")
        Component(lds, "Local Data Sources", "Local Data Logic")
        System_Ext(api, "API", "Third-Party Adventure Time API")
        ContainerDb(db, "Local Database", "Shared Preferences Cache")

        Rel(m, repo, "models are <br> passed to <br> repositories")
        UpdateRelStyle(m, repo, $textColor="lightblue" $offsetY="-40", $offsetX="-30")
        Rel(rds, m, "creates models")
        UpdateRelStyle(rds, m, $textColor="lightblue" $offsetY="0", $offsetX="-60")
        Rel(lds, m, "creates models")
        UpdateRelStyle(lds, m, $textColor="lightblue" $offsetY="0", $offsetX="-40")
        Rel(api, rds, "passes raw data retrived from the API")
        UpdateRelStyle(api, rds, $textColor="lightblue" $offsetY="0", $offsetX="-100")
        Rel(db, lds, "passes raw data retrieved from the local database")
        UpdateRelStyle(db, lds, $textColor="lightblue" $offsetY="0", $offsetX="-150")
    }
```