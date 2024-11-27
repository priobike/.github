# PrioBike

<p align="left">
  <img width="200" src="https://github.com/priobike/priobike-flutter-app/assets/27271818/096b5754-b37b-4dcb-ad76-e72edc38fc94">
  <img width="200" src="https://github.com/priobike/priobike-flutter-app/assets/27271818/32c799f9-80a5-4fcf-92c8-7ee9079dc1bd">
  <img width="200" src="https://github.com/priobike/priobike-flutter-app/assets/27271818/c2595445-dbd4-461d-9240-a9764de60faf">
</p>

<h4>The PrioBike app gives speed advisories to cyclists in Hamburg to catch green lights.</h4>

The PrioBike app allows you, as a cyclist in Hamburg, to receive traffic light information while riding. You can use this information to adjust your riding behavior. For example, you can slow down if you know the light will remain red, or speed up to catch the next green phase. The app is being developed as part of the PrioBike research project at TU Dresden to explore this innovative way of cycling in harmony with traffic lights.

## Research

If you are interested in the scientific background, we encourage you to read the following publications:

P. Matthes, "Green Light Optimal Speed Advisory for Bikes" in 2024: https://nbn-resolving.org/urn:nbn:de:bsz:14-qucosa2-925445

D. Jeschor, P. Matthes, T. Springer, S. Pape, and S. Fröhlich, “Cloudy with a Chance of Green: Measuring the Predictability of 18,009 Traffic Lights in Hamburg,” in 2024 IEEE Intelligent Vehicles Symposium (IV), IEEE, 2024, pp. 1–8. DOI: https://doi.org/10.48550/arXiv.2403.18830

P. Matthes and T. Springer, “Matching Traffic Lights to Routes for Real-World Deployments of Mobile GLOSA Apps,” in 2022 IEEE International Smart Cities Conference (ISC2), IEEE, 2022, pp. 1–7. DOI: https://doi.org/10.1109/ISC255366.2022.9922560

P. Matthes, D. Jeschor, and T. Springer, “GeoAI-Powered Lane Matching for Bike Routes in GLOSA Apps,” in The 31st ACM International Conference on Advances in Geographic Information Systems (SIGSPATIAL ’23), ACM, 2023, pp. 1–4. DOI: https://doi.org/10.1145/3589132.3625583

P. Matthes, T. Springer, and D. Jeschor, “Accurate Bike Routing for Lane Prediction in GLOSA Apps via Infrastructure Reference Models,” in 2023 IEEE In- ternational Conference on Intelligent Transportation Systems (ITSC), IEEE, 2023, pp. 1–6. DOI: https://doi.org/10.1109/ITSC57777.2023.10422472

## Contributing

We invite you to improve our app and reuse our services. Almost all of our services are public under `MIT` license.

If you would like to understand how the app works in general, it is recommended to check out the architecture description below and the [Flutter app repository](https://github.com/priobike/priobike-flutter-app) first. This is also the best way to start when you want to fix a bug in the app or contribute a feature. 

The development of this project came to an end in 2024.
So, we won't be able to reply to issues you may open here on GitHub.
If you have questions, you can contact the main developers via LinkedIn:
 - [Philipp Matthes](https://de.linkedin.com/in/pmatthes)
 - [Daniel Jeschor](https://de.linkedin.com/in/daniel-jeschor)
 - [Paul Pickhardt](https://de.linkedin.com/in/paul-pickhardt-72812521a)

## Architecture

The best way to understand the app's architecture is by looking at the three key views: the home view, the routing view, and the ride view. The home view serves as an entrypoint when opening the app, providing users with their custom routes and also some important system status information. Transitioning to the routing view, users can freely plan a route through Hamburg. Finally, in the ride view, users obtain a speed advisory for the traffic lights along the planned route. To provide these services the app uses the following basic system architecture:

![architecture-readme](https://github.com/priobike/.github/assets/27271818/a7b832fd-2435-4967-8706-1ccd437eb61a)

At its foundation, the app uses [real-time traffic light data from the Urban Data Platform in Hamburg](https://metaver.de/trefferanzeige?docuuid=AB32CF78-389A-4579-9C5E-867EF31CA225) and [generates predictions](https://github.com/priobike/priobike-predictor) based on this data. The availability of predictions is monitored, displaying a warning in the home view in case there is an outage.

The routing view is an essential part of the app, as it not only [calculates accurate bike routes through Hamburg using our DRN GraphHopper](https://github.com/priobike/priobike-graphhopper-drn) but also [matches all traffic lights to these routes in advance with our SG Selector](https://github.com/priobike/priobike-sg-selector). As in other cycling apps, additional path information is highlighted along routes and users can search for addresses, adding them to their planned route.

When a route is selected, the ride view determines the position of the user along the route, looking up which traffic lights will be passed next. The app connects to an MQTT broker that provides the generated traffic light predictions, highlighting them in a speedometer. When a ride is finished, the tracking data is uploaded to the [tracking service](https://github.com/priobike/priobike-tracking-service).

## Setup

To run the PrioBike-services on your own, a good entrypoint is the [priobike-k8s-deployment](https://github.com/priobike/priobike-k8s-deployment) repository.

## General Project

For more information on other areas of the PrioBike project see the projects [website](https://www.hamburg.de/politik-und-verwaltung/behoerden/bvm/die-themen-der-behoerde/intelligente-verkehrssysteme/priobike-192572) of the city of Hamburg.

## Acknowledgments

The PrioBike project is funded by the Federal Ministry for Digital and Transport (BMDV, FKZ: 16DKVM001B).
