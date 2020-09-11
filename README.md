# Turo2 - Repo name
This repo is accomplish the interview tasks.

## Prerequisities 
1. EKS cluster setup.
2. Have the *kubeconfig* file to access the cluster.
3. Argo CD already installed on the cluster.
   Following the instructions: https://argoproj.github.io/argo-cd/getting_started/
4. RDS cluster and DB created, provided with credentials.

## Usage
**Note:** Argo CD has an app - `wordpress` configured to use this repo as source of truth. 
Please try to run the sync first and then dry-run for testing it prior to deployment.

## Explanation

**Note:** All the objects discussed below are created in the **namespace: `argocd`**.

The repo has the required config files to deploy a wordpress app which connects to a local MySQL DB inside the EKS cluster.

### MySQL config

1. Create the secret to store the environmental varibales related to RDS MySQL.

### Wordpress config

1. Creting the presistent volume on a hostpath.
2. Creating the volume claim to claim the volume we created.
3. Creating the deployment for Wordpress.
4. Exposing the deployment as a service type - NodePort.

## Enivronmental Variables
1. The Wordpress deployment gets the following MySQL parametes from the secret through `secretKeyRef`
DB host from `$WORDPRESS_DB_HOST`.
DB name from `WORDPRESS_DB_NAME`.
DB username from `WORDPRESS_DB_USER`.
DB password from `WORDPRESS_DB_PASSWORD`.
2. We are using the sceret created as part of the MySQL config - `rds-pass`.

## Caution
1. If you are about to change the environmental varibales make sure to cade then as base64 and not actual strings in the [secret-mysql_rds.yaml](https://github.com/sairamkrishnavemulapalli/Turo2/blob/master/secret-mysql_rds.yaml)
2. If the secrets are mentioned as strings the deployment fails due to not able to code the strings with base 64.
