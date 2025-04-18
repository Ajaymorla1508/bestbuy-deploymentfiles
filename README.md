# BestBuy Cloud Native Application
Welcome to the BestBuy cloud native application application.

This application is inspired by Azure Kubernetes Service (AKS) quickstart demo [Azure Kubernetes Service (AKS) Docs](https://learn.microsoft.com/en-us/azure/aks/).

## Architecture

The application has the following services: 

| Service | Description | Github Repo |
| --- | --- | --- |
| `store-front` | Web app for customers to place orders (Vue.js) | [store-front](https://github.com/Saikarthick07/BestBuy-store-front.git) |
| `store-admin` | Web app used by store employees to view orders in queue and manage products (Vue.js) | [store-admin](https://github.com/Saikarthick07/BestBuy-store-admin.git) |
| `order-service` | This service is used for placing orders (Javascript) | [order-service](https://github.com/Saikarthick07/BestBuy-order-service.git) |
| `product-service` | This service is used to perform CRUD operations on products (Rust) | [product-service](https://github.com/Saikarthick07/BestBuy-product-service.git) |
| `makeline-service` | This service handles processing orders from the queue and completing them (Golang) | [makeline-service](https://github.com/Saikarthick07/BestBuy-makeline-service.git) |
| `ai-service` | Optional service for adding generative text and graphics creation (Python) | [ai-service](https://github.com/Saikarthick07/BestBuy-ai-service.git) |
| `mongodb` | MongoDB instance for persisted data | [mongodb](https://github.com/docker-library/mongo) |



![Logical Application Architecture Diagram](https://github.com/Saikarthick07/bestbuy-deploymentfiles/blob/main/assets/bestbuy-system-architecture.png)

## Run the app on Azure Kubernetes Service (AKS)

You can use the kubernetes YAML files provided in the [Deployment Files](./Deployment%20Files/) folder to deploy the app to an AKS cluster.



