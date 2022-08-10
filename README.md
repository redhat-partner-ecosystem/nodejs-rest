
## README

Example nodejs REST/CRUD Application. The original code can be found at [nodeshift-starters/nodejs-rest-http-crud](https://github.com/nodeshift-starters/nodejs-rest-http-crud).

### Getting Started

feature-1, added a patch
feature-2, started, added some more, some more to f2
added to develop directly,2
feature-3 ...

#### Running Locally

First, install the dependencies

`npm install`

A Postgres DB is needed, so if you are using Docker, then you can start a postgres db easily.

`docker run --name os-postgres-db -e POSTGRESQL_USER=luke -e POSTGRESQL_PASSWORD=secret -e POSTGRESQL_DATABASE=my_data -d -p 5432:5432 centos/postgresql-10-centos7`

In this example, the db user is `luke`, the password is `secret` and the database is `my_data`

You can then start the application like this:

`DB_USERNAME=luke DB_PASSWORD=secret ./bin/www`


Then go to http://localhost:8080


#### Running on Openshift

First, make sure you have an instance of Openshift setup and are logged in using `oc login`.

Then create a new project using the `oc` commands

`oc new-project fun-node-fun`

For this example, you will also need a postgres db running on your Openshift cluster.

`oc new-app -e POSTGRESQL_USER=luke -ePOSTGRESQL_PASSWORD=secret -ePOSTGRESQL_DATABASE=my_data centos/postgresql-10-centos7 --name=my-database`

Then run `npm run openshift` to deploy your app

Then you can navigate to the newly exposed route, something similar to "http://nodejs-rest-http-crud-boosters.192.168.99.100.nip.io/",  this will probably be different based on your Openshift IP address

#### Running on Openshift with traces enabled

Log in with kubeadmin and install the [`OpenShift Distributed Tracing Platform Operator`](https://docs.openshift.com/container-platform/4.10/distr_tracing/distr_tracing_install/distr-tracing-deploying-jaeger.html) and [`OpenShift Distributed Tracing Data Collection Operator (Technology Preview)`](https://docs.openshift.com/container-platform/4.10/distr_tracing/distr_tracing_install/distr-tracing-deploying-otel.html) via operator hub.
 
Then create a new project using the `oc` commands

```
oc new-project opentel
```

Give to `developer` user admin rights on the project

```
oc policy add-role-to-user admin developer -n opentel
```

Create a Jaeger instance

```
oc apply -f tracing/jaeger.yml
```

Create an OpenTelemetry instance

```
oc apply -f tracing/opentel-collector.yml
```
