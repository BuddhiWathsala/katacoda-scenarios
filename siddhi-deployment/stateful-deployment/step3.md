This section provides instructions on deploying the stateful Siddhi App that was discussed in the Introduction section.

### Deploy Siddhi App

Retrieve a prewritten SiddhiProcess YAML, with the earlier discussed `PowerConsumptionSurgeDetection` Siddhi App, using the following command.

`wget https://raw.githubusercontent.com/siddhi-io/katacoda-scenarios/master/siddhi-deployment/stateful-deployment/power-consume-app.yaml`{{execute}}

Run the following command to view the SiddhiProcess YAML.

`cat power-consume-app.yaml`{{execute}}

Here, the App is parametrized to retrieve the `RECEIVER_URL` from environment variables, and configured to be deployed using `siddhiio/siddhi-runner-ubuntu:5.1.2` docker image. 

Further, to persist the periodic states produced by Siddhi, a persistent volume claim is configured under the `persistentVolume` section, and the relevant persistent configuration of the Siddhi runner is provided under the `runner` section.

Deploy the Siddhi SiddhiProcess using the below command.

`kubectl apply -f power-consume-app.yaml`{{execute}}

### Validate the deployment

The status of the `SiddhiProcess` can be viewed using the following commands.

`kubectl get siddhi`{{execute}}

The generated results will be similar to the following. 

```sh
$ kubectl get siddhi

NAME                STATUS    READY    AGE
power-consume-app    Ready     1/1      5m
```

Make sure the `power-consume-app` is in the `Ready` state. The `Ready` state is the indication that the Siddhi app is deployed correctly and ready to consume external requests.

**Note:** The Siddhi Operator parses and validates Siddhi Apps before deploying them. This is done by temporarily deploying a parser with a name `power-consume-app-parser`, and removing after parsing.

The next section provides information on testing the stateful Siddhi App.

