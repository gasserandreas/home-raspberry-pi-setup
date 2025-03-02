# Airflow Docker Environment

Airflow Docker environment for Raspberry PI.

## How to install

1. checkout repository
2. rename `.env.example` to `.env` and add credentials
3. create `data` folder: `mkdir data`
4. clone airflow-repo into data folder: `cd ./data && git clone git@github.com:gasserandreas/home-airflow-data.git`
5. go back to root folder: `cd ../`
6. continue with "How to start"

## How to start

1. start local environment with docker: `docker compose up -d`

## How to start after update

1. run: `docker-compose up --build -d`

## Troubleshoot

How to check logs of Docker service: `docker compose logs {service-name}`