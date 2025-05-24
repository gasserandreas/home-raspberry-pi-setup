# Home API Environment

Home API Docker environment for Raspberry PI.

## How to install

1. checkout repository
2. clone home-api into root folder: `git clone git@github.com:gasserandreas/home-api.git`
3. rename `.env.example` to `.env` and add credentials
4. continue with "How to start"

## How to start

1. start local environment with docker: `docker compose up -d`

## How to start after update

1. run: `docker compose up --build -d`

## Troubleshoot

How to check logs of Docker service: `docker compose logs {service-name}`