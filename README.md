# Example of E2E Tests with Docker Compose

## How to Run

- To start the services run `docker compose up` or `sh start-docker-environment.sh`. You can then access the frontent in your browser on `http://localhost:30002` and log in with username `testuser` and password `test123`.
- To run the E2E test in Docker Compose run `sh run-tests-in-docker.sh`.
- To run the tests locally with the test UI, run `cd tests && yarn start`.

## The Example Application

In this repo you will find a simple crypto currency tracker application, consisting of 2 services. A frontend and a backend.

```mermaid
flowchart TD
    A[Frontend] --> B[Backend]
    B[Backend] -->|gets prices from| D[Coinbase API]
    B[Backend] -->|persists user's currencies| E[Mongo DB]
```

The application lets you "track" the price of crypto currencies, by storing a list of the user's selected currencies and fetching the latest market prices from [Coinbase](https://www.coinbase.com/). The user can follow the price change since the currency was first "tracked".

The application requires authentication, which is provided by the MongoDB authenticated user system.

The goal of the application architecture is to provide a scaled down example of a production-like system. Where you have authentication, multiple services, external dependencies and persistance.

## The E2E Tests

For this Demo we're using [Cypress](https://www.cypress.io/) as our tests automation framework. But in practice any modern E2E-testing framework support the techniques being demonstrated here.

The goal is to demonstrate how Docker, and Docker Compose, can assist in creating a reproducable test environment that will perform in the same way regardless of it's being executed on a developer's machine or in a CI pipeline.

The final test infrastructure looks like this

```mermaid
flowchart TD
    T[Tests] --> A[Frontend]
    A[Frontend] --> B[Backend]
    B[Backend] -->|gets prices from| D[Mocked Coinbase API]
    B[Backend] -->|persists user's currencies| E[Mongo DB]
```
