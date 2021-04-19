# Crosswork Network Controller 2.0 Active Topology API Overview

The document contains CNC Active Topology APIs. The APIs are available only when “Active Topology” application is installed. Please refer to the installation document on how to install Crosswork Network Controller application “Active Topology”.

## Cisco NSO Connector API

APIs to control synchronization between Cisco Crosswork Controller and NSO service inventory.

## Cisco NSO RESTCONF API

Describe how to use the NSO RESTCONF API with CNC Active Topology endpoint on Cisco Crosswork Controller API Gateway.

## FP Deployment Manager API

APIs to show Active Topology Function Pack deployment information and switch between IETF NM models and Cisco Flat Models for VPN services.

## Service Inventory APIs

For VPN Services API,  default supported models are IETF models. To use the Cisco Flat Model API which are included but not activated, user  need to perform explicit activation. When Cisco Flat Models are activated, IETF models will be de-activated and cannot be used. It is recommended to use only IETF models as they are default supported model. Please refer to CNC 2.0 user and admin guides on how to switch model activations.

### Flat L2VPN Service API

APIs to read, create, modify and delete L2VPN service with Flat model.
Please note, the APIs are applicable only when Flat L2VPN Service model is installed and activated.

### Flat L3VPN Service API

APIs to read, create, modify and delete L3VPN service with Flat model.
Please note, the APIs are applicable only when Flat L3VPN Service model is installed and activated.

### IETF L2VPN Service API

APIs to read, create, modify and delete L2VPN service with IETF model.
Please note, the APIs are applicable only when NM L2VPN Service model is installed and activated.

### IETF L3VPN Service API

APIs to read, create, modify and delete L3VPN service with IETF model.
Please note, the APIs are applicable only when NM L3VPN Service model is installed and activated.

### RSVP-TE API

APIs to read, create, modify and delete RSVP-TE tunnel.

### Service Summary API

APIs to read service summary.

### SR-TE Policy API

APIs to read, create, modify and delete SR-TE policy.
