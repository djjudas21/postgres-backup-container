# Container to create PostgreSQL Backups
Minimalistic container for backing up PostgreSQL databases.

## Goal

Easily backup your PostgreSQL Database. 

Intended to be used with: 
1. Kubernetes for creating CronJobs that periodically back up your database.
2. Container Instances (e.g Azure Container Instances, AWS Fargate) that can be scheduled at specified times.
3. Your computer! It's smaller than pgAdmin.  

## Environment Variables

* `PGHOST` (default: `localhost`)
* `PGPORT` (default: `5432`)
* `PGDATABASE` (default: `postgres`)
* `PGUSER` (default: `postgres@postgres`)
* `PGPASSWORD` (default: `password`)

## Tags

This image is tagged with the same major versions as Postgres (currently, `9`, `10` and `11`). You must specify the tag
to match your Postgres database server.

## Running the Backup CronJob in Kubernetes

1. Replace database creds in [pg-backup-cronJob.yaml](./kubernetes/pg-backup-cronJob.yaml).
**Attention**: This example is for simplicity, and these should be replaced with Secrets in a production environment.

Run this command to create your Kubernetes resources:

```sh
kubectl create -f ./kubernetes
```

## Running manually on your computer

```sh
docker run -v /host/backup:/pg_backup djjudas21/postgres-backup
```

## Contributing and Modifying

1. Make your desired changes and build the container:

`docker build -t $DOCKER_USER/postgres-backup .`

2. Test it locally by executing the command below:

`docker run -v /host/backup:/pg_backup $DOCKER_USER/postgres-backup`

3. Verify that it is an improvement and commit your changes ;)
