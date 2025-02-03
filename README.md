# Windmill on Render

This is a simple setup for running Windmill on Render.

## Setup

- On your Render dashboard, create a "Blueprint" (click + New on the top right of the dashboard).
- Select this github repository as the source.
- If you do not have an exsting S3 bucket, setup MinIO as instance storage.
  - Connect to the MinIO console server and use the credentials provided in the service details "Environment Variables"
  - Create a bucket `windmill-instance-storage`
  - Create an access key and secret key in the MinIO console server "Access Keys" setting and copy them
  - Click "Create"
  - Go to the Windmill "instance settings" and in the "Core" tab, set the "Instance Objext Storage" to "S3" and add
    -  Bucket: `windmill-instance-storage`
    -  Access Key ID: `access key id`
    -  Secret Access Key: `secret access key`
    -  Region: `region`
    -  Endpoint: `<minio server url>:9000`
    -  Allow http: `true`
  - Click "Test from a server" and "Test from a worker" and make sure they both succeed
  - Click "Save"
 
## Community Edition
  - If using the Windmill CE, you will have to change the image from `windmill-ee:main` to `windmill:main`
  - LSP, Multiplayer and Indexer are only supported in the Enterprise Edition so you'll have to comment out those services
    - in [render.yaml](./render.yaml)
    - in [Caddyfile](./Caddyfile)
 
## NOTES
- Render does not forward SMTP traffic to services hosted on Render. Hence, [Email Triggers](https://www.windmill.dev/docs/getting_started/triggers#emails) will not be supported. Instead, you can use an external email service such as gmail etc. and use their APIs.
