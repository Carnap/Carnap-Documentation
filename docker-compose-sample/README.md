# Carnap docker-compose sample

This is a sample using docker-compose to deploy Carnap to a Docker host, using
PostgreSQL as a database and Caddy to terminate HTTPS connections. These are only a
sample of how to configure an instance: you can equally use nginx or any other
reverse proxy to terminate HTTPS.

This configuration assumes you don't have anything running on ports 80 or 443.
If you already have a web server, remove the Caddy container and use your
existing web server to reverse proxy Carnap.

## Usage

1. Set up DNS records for the domain name for your instance to point at the
   machine you're running Carnap on.

2. Copy the example files (each command is on a line starting with `$ `):
   ```
   # Grab the files
   $ git clone https://github.com/Carnap/Carnap-Documentation carnap-docs
   $ cp -R carnap-docs/docker-compose-sample carnap-docker-compose

   $ cd carnap-docker-compose
   $ cp .env.example .env
   $ cp .env-postgres.example .env-postgres
   ```

3. Fill in the details of your installation in the below list of files. See
   [the administration guide](https://carnap.io/srv/doc/administration.md) for
   details on setting up Google login.

   - [ ] `Caddyfile` (email address, domain name)
   - [ ] `.env` (new postgres password, Google login details)
   - [ ] `.env-postgres` (same postgres password as `.env`)

4. Run `docker-compose up`.
