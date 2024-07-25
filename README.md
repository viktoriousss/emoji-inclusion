
This app can be used to demo Tanzu Platform for K8S

Check (.tanzu/config)[https://github.com/viktoriousss/emoji-inclusion/tree/main/.tanzu/config] to see specific configuration settings.

Original app + idea coming from (Timo Salm)[https://github.com/timosalm/emoji-inclusion]

## Example 1

Build and deploy the app:
```
tanzu deploy -y
```

# Example 2

Build the app:
```
tanzu build --output-dir ~/build
```
Now deploy the app:
```
tanzu deploy --from-build ~/build -y
```

# Example 3
Bind a persistent DB to the app (using Dynamic provisioning with Bitnami)

Show available service types:
```
tanzu service type list
```

Create a PostgreSQL instance:
```
tanzu service create PostgreSQLInstance/my-db
```

Bind it to the app:
```
tanzu service bind PostgreSQLInstance/my-db ContainerApp/emoji-inclusion --as db
```

Don't forget to unbind when finished:
```
tanzu service unbind PostgreSQLInstance/my-db ContainerApp/emoji-inclusion
```

Delete the service:
```
tanzu service delete PostgreSQLInstance/my-db
```

# Example 4
Bind a pre-povisioned presistent DB to the app


Create the secret:
```
kubectl apply -f preprovisioned-db-secret.yaml
```

Deploy the database:
```
kubectl apply -f .tanzu/config/preprovisioned-db.yaml
```

Bind the shared database to the app:
```
tanzu service bind PreProvisionedService/shared-postgres ContainerApp/emoji-inclusion --as db
```