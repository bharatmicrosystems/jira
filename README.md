# jira
Atlassian Jira Kubernetes config

## Quick Start
```
git clone https://github.com/bharatmicrosystems/jira.git
cd jira
kubectl apply -f jira.yaml
```
This would perform the following steps

1. Create a persistent volume called jira-pv-volume with a path to /kubevolumes/jira_data. This would ensure that the jira-data is persisted on disk even if the jira container goes down. The disk is replicated across all the nodes so the container can be scheduled to any of the nodes in the cluster
2. Create a persistent volume claim called jira-pv-claim which binds with jira-pv-volume
3. Create the jira stateful set which contains a reference to the official jira container provided by atlassian and the /jira-data volume mounted to jira-pv-claim.
4. Create a cluster IP service to expose the jira UI to the kubernetes cluster
5. Create an ingress service to expose the jira UI to the outside world on jira.example.com on port 80.

## Further setup
Access Jira from the browser and follow on-screen instructions.

When prompted for choosing the type of configuration, choose "Configure everything myself"

In the database-configuration choose my own database, use database PostgreSQL (Ensure that you have already setup postgres by using https://github.com/bharatmicrosystems/postgres.git)

1. Hostname - postgres-jiraconfluence-service
2. Port - 5432
3. Database - jira2db
4. User - jira2dbuser

Forward and paste the license key
