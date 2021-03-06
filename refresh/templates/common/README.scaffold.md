## Scaffolded Swift Kitura server application

[![](https://img.shields.io/badge/bluemix-powered-blue.svg)](https://bluemix.net)
[![Platform](https://img.shields.io/badge/platform-swift-lightgrey.svg?style=flat)](https://developer.ibm.com/swift/)

### Table of Contents
* [Summary](#summary)
* [Requirements](#requirements)
* [Project contents](#project-contents)
* [Configuration](#configuration)
* [Run](#run)
* [Deploy to IBM Cloud](#deploy-to-ibm-cloud)
* [License](#license)
* [Generator](#generator)

### Summary
This scaffolded application provides a starting point for creating Swift applications running on [Kitura](http://www.kitura.io/).

### Requirements
* [Swift 4](https://swift.org/download/)

### Project contents
This application has been generated with the following capabilities and services:

* [CloudEnvironment](#configuration)
<% if (web) { -%>
* [Static web file serving](#static-web-file-serving)
<% } -%>
<% if (hostSwagger) { -%>
* [OpenAPI / Swagger endpoint](#openapi--swagger-endpoint)
<% } -%>
<% if (exampleEndpoints) { -%>
* [Example endpoints](#example-endpoints)
<% } -%>
<% if (metrics) { -%>
* [Embedded metrics dashboard](#embedded-metrics-dashboard)
<% } -%>
<% if (docker) { -%>
* [Docker files](#docker-files)
<% } -%>
* [Iterative Development](#iterative-development)
* [IBM Cloud deployment](#ibm-cloud-deployment)
<% if (cloudant) { -%>
* [Cloudant](#cloudant)
<% } -%>
<% if (redis) { -%>
* [Redis](#redis)
<% } -%>
<% if (objectStorage) { -%>
* [Object Storage](#object-storage)
<% } -%>
<% if (auth) { -%>
* [AppID](#appid)
<% } -%>
<% if (conversation) { -%>
* [Watson Conversation](#watson-conversation)
<% } -%>
<% if (alertNotification) { -%>
* [Alert Notification](#alert-notification)
<% } -%>
<% if (push) { -%>
* [Push Notifications](#push-notifications)
<% } -%>
<% if (autoscaling) { -%>
* [Auto-scaling](#auto-scaling)
<% } -%>

<% if (web) { -%>
#### Static web file serving
This application includes a `public` directory in the root of the project. The contents of this directory will be served as static content using the built-in Kitura [StaticFileServer module](https://github.com/IBM-Swift/Kitura/wiki/Serving-Static-Content).

This content is hosted on `/`. For example, if you want to view `public/myfile.html` and the application is hosted at https://localhost:8080, go to https://localhost:8080/myfile.html.
<% } -%>
<% if (hostSwagger) { -%>
#### OpenAPI / Swagger endpoint
This application hosts an endpoint for serving the OpenAPI Swagger definition for this application. It expects the definition file to be located in `definitions/<%- appName %>.yaml`.

The endpoint is hosted on `/swagger/api`. For example, if the application is hosted at https://localhost:8080, go to https://localhost:8080/swagger/api.
<% } -%>
<% if (exampleEndpoints) { -%>
#### Example endpoints
This application includes an OpenAPI Swagger definition and routes for a Product example resource. The OpenAPI Swagger definition is located in the `definitions/<%- appName %>.yaml` directory.

<%   if (hostSwagger) { -%>
The specification of this interface is made available through an embedded Swagger UI hosted on `/explorer`. For example, if the application is hosted at https://localhost:8080, go to https://localhost:8080/explorer.

The Swagger UI will document the paths and http methods that are supported by the application.
<%   } -%>
<% } -%>
<% if (metrics) { -%>
#### Embedded metrics dashboard
This application uses the [SwiftMetrics package](https://github.com/RuntimeTools/SwiftMetrics) to gather application and system metrics.

These metrics can be viewed in an embedded dashboard on `/swiftmetrics-dash`. The dashboard displays various system and application metrics, including CPU, memory usage, HTTP response metrics and more.
<% } -%>
<% if (docker) { -%>
#### Docker files
The application includes the following files for Docker support:
* `.dockerignore`
* `Dockerfile`
* `Dockerfile-tools`

The `.dockerignore` file contains the files/directories that should not be included in the built docker image. By default this file contains the `Dockerfile` and `Dockerfile-tools`. It can be modified as required.

The `Dockerfile` defines the specification of the default docker image for running the application. This image can be used to run the application.

The `Dockerfile-tools` is a docker specification file similar to the `Dockerfile`, except it includes the tools required for compiling the application. This image can be used to compile the application.

Details on how to build the docker images, compile and run the application within the docker image can be found in the [Run section](#run) below.
<% } -%>
#### IBM Cloud deployment
Your application has a set of cloud deployment configuration files defined to support deploying your application to IBM Cloud:
* `manifest.yml`
* `.bluemix/toolchain.yml`
* `.bluemix/pipeline.yml`

The [`manifest.yml`](https://console.ng.bluemix.net/docs/manageapps/depapps.html#appmanifest) defines options which are passed to the Cloud Foundry `cf push` command during application deployment.

[IBM Cloud DevOps](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html) service provides toolchains as a set of tool integrations that support development, deployment, and operations tasks inside IBM Cloud, for both Cloud Foundry and Kubernetes applications. The ["Create Toolchain"](#deploy-to-ibm-cloud) button creates a DevOps toolchain and acts as a single-click deploy to IBM Cloud including provisioning all required services.

<% if (cloudant) { -%>
#### Cloudant
This application uses the [Kitura-CouchDB package](https://github.com/IBM-Swift/Kitura-CouchDB), which allows Kitura applications to interact with a Cloudant or CouchDB database.

CouchDB speaks JSON natively and supports binary for all your data storage needs.

Boilerplate code for creating a client object for the Kitura-CouchDB API is included inside `Sources/Application/Application.swift` as an `internal` variable available for use anywhere in the `Application` module.

The connection details for this client are loaded by the [configuration](#configuration) code and are passed to the Kitura-CouchDB client in the boilerplate code.
<% } -%>
<% if (redis) { -%>
#### Redis
This application uses the [Kitura-redis](http://ibm-swift.github.io/Kitura-redis/) library, which allows Kitura applications to interact with a Redis database.

Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache and message broker. It supports a cracking array of data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries.

Boilerplate code for creating a client object for the Kitura-redis API is included inside `Sources/Application/Application.swift` as an `internal` variable available for use anywhere in the `Application` module.

The connection details for this client are loaded by  the [configuration](#configuration) code and are passed to the Kitura-redis client in the boilerplate code.
<% } -%>
<% if (objectStorage) { -%>
#### Object Storage
This application uses the [Object Storage package](https://github.com/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift.git) to connect to the IBM Cloud Object Storage service.

Object Storage provides an unstructured cloud data store, which allows the application to store and access unstructured data content.

Boilerplate code for creating a client object for the Object Storage API is included inside `Sources/Application/Application.swift` as an `internal` variable available for use anywhere in the `Application` module.

The connection details for this client are loaded by the [configuration](#configuration) code and are passed to the Object Storage client in the boilerplate code.
<% } -%>
<% if (auth) { -%>
#### AppID
This application uses [App ID package](https://github.com/ibm-cloud-security/appid-serversdk-swift) to connect to the IBM Cloud App ID service.

App ID provides authentication to secure your web applications and back-end systems. In addition App ID supports authentication using social identity providers so that users can login with their existing user accounts, such as Facebook and Google.

Boilerplate code for creating a client object for the App ID API is included inside `Sources/Application/Application.swift` as an `internal` variable available for use anywhere in the `Application` module. Extra routes and logic need to be added to make this a authentication boilerplate work. A working example can be found in the [App ID README](https://github.com/ibm-cloud-security/appid-serversdk-swift/blob/master/README.md#example-usage).

The connection details for this client are loaded by the [configuration](#configuration) code and are passed to the App ID client in the boilerplate code.
<% } -%>
<% if (conversation) { -%>
#### Watson Conversation
This application uses the [Watson Swift SDK package](https://github.com/watson-developer-cloud/swift-sdk), which allows Kitura applications to build Watson-powered applications, specifically in this case the IBM Watson Conversation service.

With the IBM Watson Conversation service you can create cognitive agents--virtual agents that combine machine learning, natural language understanding, and integrated dialog scripting tools to build outstanding projects, such as a chat room with an integrated Watson chat bot.

Boilerplate code for creating a client object for the Watson Conversation API is included inside `Sources/Application/Application.swift` as an `internal` variable available for use anywhere in the `Application` module.

The connection details for this client are loaded by the [configuration](#configuration) code and are passed to the Watson Conversation client in the boilerplate code.

More information about the Watson Conversation can be found in the [README](https://github.com/watson-developer-cloud/swift-sdk#conversation).
<% } -%>
<% if (alertNotification) { -%>
#### Alert Notification
This application uses the [Alert Notification Service SDK package](https://github.com/IBM-Swift/alert-notification-sdk), which allows Swift developers to utilize the Alert Notifications service in their applications, allowing for the proactive remediation of issues for applications running on IBM Cloud. Alerts and messages can be created, received and deleted through the use of this SDK.

This SDK is for the consumption/usage of the Alert Notification service and not for administration of the service. Adding users, groups, notification policies, etc. should be done through the IBM Cloud dashboard.

Boilerplate code for creating a client object for the Alert Notification API is included inside `Sources/Application/Application.swift` as an `internal` variable available for use anywhere in the `Application` module.

The connection details for this client are loaded by the [configuration](#configuration) code and are passed to the Alert Notification client in the boilerplate code.

A quick start guide to the Alert Notification Service on IBM Cloud can be found  [here](https://www.ibm.com/blogs/bluemix/2015/12/quick-start-guide-to-alert-notification-service/).
<% } -%>
<% if (push) { -%>
#### Push Notifications
This application uses the [Push notifications package](https://github.com/ibm-bluemix-mobile-services/bms-pushnotifications-serversdk-swift), which is a Swift server-side SDK for sending push notifications via the IBM Cloud Push Notifications services.

Boilerplate code for creating a client object for the Push Notifications API is included inside `Sources/Application/Application.swift` as an `internal` variable available for use anywhere in the `Application` module.

The connection details for this client are loaded by the [configuration](#configuration) code and are passed to the Push Notifications client in the boilerplate code.
<% } -%>
<% if (autoscaling) { -%>
#### Auto-scaling
This application uses the [SwiftMetrics package](https://github.com/RuntimeTools/SwiftMetrics) for connecting to the IBM Cloud Auto-scaling service. You can use this to automatically manage your application capacity when deployed to the cloud.  You will need to define the Auto-Scaling policy (https://console.ng.bluemix.net/docs/services/Auto-Scaling/index.html) to define the rules used to scale the application.

The connection details for this client are loaded by the [configuration](#configuration) code and are passed to the SwiftMetrics auto-scaling client in the boilerplate code.
<% } -%>

### Configuration
Your application configuration information is stored in the `config.json` in the project root directory. This file is in the `.gitignore` to prevent sensitive information from being stored in git.

The connection information for any configured services, such as username, password and hostname, is stored in this file.

The application uses the [CloudEnvironment package](https://github.com/IBM-Swift/CloudEnvironment) to read the connection and configuration information from the environment and this file.

If the application is running locally, it can connect to IBM Cloud services using unbound credentials read from this file. If you need to create unbound credentials you can do so from the IBM Cloud web console ([example](https://console.ng.bluemix.net/docs/services/Cloudant/tutorials/create_service.html#creating-a-service-instance)), or using the CloudFoundry CLI [`cf create-service-key` command](http://cli.cloudfoundry.org/en-US/cf/create-service-key.html).

When you push your application to IBM Cloud, these values are no longer used, instead the application automatically connects to bound services using environment variables.

### Run
To build and run the application:
1. `swift build`
1. `.build/debug/<%- executableName %>`

<% if (metrics) { -%>
**NOTE**: On macOS you will need to add options to the `swift build` command: `swift build -Xlinker -lc++`
<% } -%>

<% if (docker) { -%>
#### Docker
To build the two docker images, run the following commands from the root directory of the project:
* `docker build -t myapp-run .`
* `docker build -t myapp-build -f Dockerfile-tools .`
You may customize the names of these images by specifying a different value after the `-t` option.

To compile the application using the tools docker image, run:
* `docker run -v $PWD:/swift-project -w /swift-project myapp-build /swift-utils/tools-utils.sh build release`

To run the application:
* `docker run -it -p 8080:8080 -v $PWD:/swift-project -w /swift-project myapp-run sh -c .build-ubuntu/release/<%- executableName %>`
<% } -%>

#### Iterative Development
The `iterative-dev.sh` script is included in the root of the generated Swift project and allows for fast & easy iterations for the developer. Instead of stopping the running Kitura server to see new code changes, while the script is running, it will automatically detect changes in the project's **.swift** files and recompile the app accordingly.

To use iterative development:
* For native OS, execute the `./iterative-dev.sh` script from the root of the project.
<% if (docker) { -%>
* With docker, shell into the tools container mentioned above, and run the `./swift-project/iterative-dev.sh` script.  File system changes are detected using a low-tech infinitely looping poll mechanism, which works in both local OS/filesystem and across host OS->Docker container volume scenarios.
<% } -%>

### Deploy to IBM Cloud
You can deploy your application to Bluemix using:
* the [CloudFoundry CLI](#cloudfoundry-cli)
* an [IBM Cloud toolchain](#ibm-cloud-toolchain)

#### CloudFoundry CLI
You can deploy the application to IBM Cloud using the CloudFoundry command-line:
1. Install the Cloud Foundry command-line (https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
1. Ensure all configured services have been provisioned
1. Run `cf push` from the project root directory

The Cloud Foundry CLI will not provision the configured services for you, so you will need to do this manually using the IBM Cloud web console ([example](https://console.ng.bluemix.net/docs/services/Cloudant/tutorials/create_service.html#creating-a-service-instance)) or the CloudFoundry CLI (`cf create-service` command)[http://cli.cloudfoundry.org/en-US/cf/create-service.html]. The service names and types will need to match your [configuration](#configuration).

#### IBM Cloud toolchain
You can also set up a default IBM Cloud Toolchain to handle deploying your application to IBM Cloud. This is achieved by publishing your application to a publicly accessible github repository and using the "Create Toolchain" button below. In this case configured services will be automatically provisioned, once, during toolchain creation.

[![Create Toolchain](https://console.ng.bluemix.net/devops/graphics/create_toolchain_button.png)](https://console.ng.bluemix.net/devops/setup/deploy/)

### License
All generated content is available for use and modification under the permissive MIT License (see `LICENSE` file), with the exception of SwaggerUI which is licensed under an Apache-2.0 license (see `NOTICES.txt` file).

### Generator
This project was generated with [generator-swiftserver](https://github.com/IBM-Swift/generator-swiftserver) v<%- generatorVersion %>.
