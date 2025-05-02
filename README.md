# geonode_platform

GeoNode template project. Generates a django project with GeoNode support.

## Table of Contents

-  [Quick Docker Start](#quick-docker-start)
-  [Developer Workshop](#developer-workshop)
-  [Create a custom project](#create-a-custom-project)
-  [Start your server using Docker](#start-your-server-using-docker)
-  [Run the instance in development mode](#run-the-instance-in-development-mode)
-  [Run the instance on a public site](#run-the-instance-on-a-public-site)
-  [Stop the Docker Images](#stop-the-docker-images)
-  [Backup and Restore from Docker Images](#backup-and-restore-the-docker-images)
-  [Recommended: Track your changes](#recommended-track-your-changes)
-  [Hints: Configuring `requirements.txt`](#hints-configuring-requirementstxt)

## Quick Docker Start

 Generate the .env file

  ```bash
    python create-envfile.py 
  ```

`create-envfile.py` accepts the following arguments:

- `--https`: Enable SSL. It's disabled by default
- `--env_type`: 
   - When set to `prod` `DEBUG` is disabled and the creation of a valid `SSL` is requested to Letsencrypt's ACME server
   - When set to `test`  `DEBUG` is disabled and a test `SSL` certificate is generated for local testing
   - When set to `dev`  `DEBUG` is enabled and no `SSL` certificate is generated
- `--hostname`: The URL that whill serve GeoNode (`localhost` by default)
- `--email`: The administrator's email. Notice that a real email and a valid SMPT configurations are required if  `--env_type` is seto to `prod`. Letsencrypt uses to email for issuing the SSL certificate 
- `--geonodepwd`: GeoNode's administrator password. A random value is set if left empty
- `--geoserverpwd`: GeoNode's administrator password. A random value is set if left empty
- `--pgpwd`: PostgreSQL's administrator password. A random value is set if left empty
- `--dbpwd`: GeoNode DB user role's password. A random value is set if left empty
- `--geodbpwd`: GeoNode data DB user role's password. A random value is set if left empty
- `--clientid`: Client id of Geoserver's GeoNode Oauth2 client. A random value is set if left empty
- `--clientsecret`: Client secret of Geoserver's GeoNode Oauth2 client. A random value is set if left empty
```bash
  docker compose build
  docker compose up -d
```