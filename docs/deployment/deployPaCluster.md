---
title: Deploy PingAccess Cluster
---
# Deploying PingAccess Cluster

This use case employs the `pingidentity-server-profiles/pa-clustering` server profile. This server profile contains an H2 database engine located in `pingidentity-server-profiles/pa-clustering/pingaccess/instance/data/PingAccess.mv.db`. H2 is configured to reference the PingAccess Admin engine at `pingaccess:9090`.

> Remember to include this if you create your own server profile. This setting is not contained in an exported PingAccess configuration archive.

## Before you begin

* You've already been through [Get Started](../get-started/introduction.md) to set up your DevOps environment and run a test deployment of the products.

## About this task

You will:

* Deploy the PingAccess cluster.
<!-- * Verify the cluster status. -->
* Replicate the cluster configuration.
* Scale the PingAccess engines.

## Deploying Cluster

Use the `docker-compose.yaml` file in your local `pingidentity-devops-getting-started/11-docker-compose/06-pingaccess-cluster` directory to deploy the cluster.

1. From the `pingidentity-devops-getting-started/11-docker-compose/06-pingaccess-cluster` directory, start the stack. Enter:

      ```sh
      docker-compose up -d
      ```

1. Check that the containers are healthy and running:

      ```sh
      docker-compose ps
      ```

      You can also display the startup logs:

      ```sh
      docker-compose logs -f
      ```

      To see the logs for a particular product container at any point, enter:

      ```sh
      docker-compose logs <product-container-name>
      ```

1. Sign on to the PingAccess Administrator Console:

      | Product | Connection Details |
      | --- | --- |
      | [PingAccess](https://localhost:9000) | <ul><li>URL: [https://localhost:9000](https://localhost:9000)</li><li>Username: administrator</li><li>Password: 2FederateM0re</li></ul> |

## Verifying Cluster Status

Check the status of the cluster using either the admin console or the Admin REST API:

* To use the Administrator Console:

      1. Sign on to the Administrator Console: `https://localhost:9000`
      1. To see your engines, go to Settings.

* To use the PingAccess Admin REST API, enter:

      ```sh
      curl -k -u administrator:2FederateM0re \
         -H 'X-XSRF-Header: PingAccess' https://localhost:9000/pa-admin-api/v3/engines
      ```

      The resulting response resembles the following:

      ```json
      {
         "items":[
            {
               "id":1,
               "name":"1e0e17125564",
               "description":null,
               "configReplicationEnabled":true,
               "keys":[
                  {
                     "jwk":{
                        "kty":"EC",
                        "kid":"41097511-9945-49df-8a43-f463fb9fe353",
                        "x":"-tZ6kNF1o2QCAK6bIG2DeGqpOnp6V6HJZcPhUJ3JbZ8",
                        "y":"lO_BkXLnGLSiC4O7TPmWBDk2YOHuqno61QInkgL7-5M",
                        "crv":"P-256"
                     },
                     "created":1582783126865
                  }
               ],
               "httpProxyId":0,
               "httpsProxyId":0,
               "selectedCertificateId":5,
               "certificateHash":{
                  "algorithm":"SHA1",
                  "hexValue":"e8a4cc6163fce9b7216b284ef635306f07be381b"
               }
            }
         ]
      }
      ```

## Scaling Engines

To scale up to two engine nodes:

```sh
docker-compose up -d --scale pingaccess-engine=2
```

## Cleaning Up

When you no longer want to run this stack, bring the stack down.

To remove all of the containers and associated Docker networks, enter:

```sh
docker-compose down
```

To stop the running stack without removing any of the containers or associated Docker networks, enter:

```sh
docker-compose stop
```

To remove attached Docker Volumes

```sh
docker volume prune
```
