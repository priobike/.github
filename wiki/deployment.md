# Deployment infrastructure

We use three separate deployments for our app: `staging`, `production`, and `release`. Each contain a similar stack of services.

## Where are services deployed?

`main/master` branches of services are deployed in `staging` for initial testing.

After testing, services are checked out into the `stable` branch, deployed in the `production` deployment. The `release` deployment is subsequentially also updated by creating a new version tag. Services running in `production` and `release` may differ slightly from each other, but must have a consistent API due to the failover, see below.

## Deployment selection

Using the "Ort" option in the internal app settings the app can switch between the deployments.

<img height="200" src="https://github.com/priobike/.github/assets/27271818/4f406508-6a87-4054-bb66-3f4de91ce3f8">

Here, Dresden points the app to the `staging` setup. 

Originally, the `production` and `release` setups were managed differently as "Hamburg (beta)" and "Hamburg (release)", but since the release of the app we use the `production` setup as a failover for the `release` setup, effectively combining both deployments. Specifically, whenever the [load service](https://github.com/priobike/priobike-load-service) running in `release` detects a high load, it triggers clients to use the `production` deployment instead.

## Staging setup

There are some additional things to consider for the staging setup:

Since the PrioBike app is developed in Dresden for the city of Hamburg, we need some deployment that can be used to test the app and its backend services without traveling to Hamburg. This is the key focus of our `staging` deployment. This deployment runs on VMs at TU Dresden and is managed by the PrioBike dev team.

The staging deployment contains services like a [traffic light data generator](https://github.com/priobike/priobike-traffic-lights-dresden) that mock the behavior of the deployment in Hamburg. For example, the traffic light geometries used by the [signal group selector](https://github.com/priobike/priobike-sg-selector) are extracted from OpenStreetMap metadata, instead of using the real MAP topologies provided by the city. Furthermore, we have two physical test traffic lights that can be setup at an arbitrary location in Dresden for additional testing. 

Additionally, the staging setup also does not use a [DRN GraphHopper](https://github.com/priobike/priobike-graphhopper-drn). Even when DRN routing is selected in the mobile app, the app will use OpenStreetMap routing and the OSM-tuned traffic light matching.
