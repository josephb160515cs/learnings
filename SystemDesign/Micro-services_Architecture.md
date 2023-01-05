# Micro-services Architecture

## Introduction
Micro-services architecture is a sytle of architecture in which in single application is developed as a suite of services.

## Features
* Small, loosely coupled services which can be handled by a small team.
* Seperate codebase for different services
* Deployed independently
* Storing their own data
* Technology agnostic 
* Services communicate via well defined APIs
* Different programming languages can be used.
* Services can be scaled independently
* Easier to implement features and bug fixes
* Fault isolation is easy

## Characteristics
* Componentization via service
* Products not Projects
* Decentralized Goverance - Netflix follows this characteristic where libraries are made open source.
* Infrastructure Automation
* Design for Failure.


## Challenges
* Complexity - Simple services but entire system is complex
* Network problems and latency
* Development and testing e2e when compared monolithic.
* Data Integrity - We should aim for eventual consistency and transaction are hard to implement

## Communication
* Uses http or gRPC