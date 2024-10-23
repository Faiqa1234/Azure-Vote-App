# Azure Vote App with Docker-Compose

This project demonstrates how to set up and run the Azure Vote app using Docker Compose. The Azure Vote app consists of a front-end web application and a back-end Redis database. This guide will help you deploy the app to Azure Container Instances (ACI).

## Prerequisites

Before you begin, ensure you have the following installed on your machine:

- Docker
- Docker Compose
- Azure CLI

## Setup

1. **Clone the repository:**

    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```

2. **Configure the `docker-compose.yaml` file:**

    Make sure your `docker-compose.yaml` file is correctly configured. Here is an example configuration:

    ```yaml
    version: '3'

    services:
      redis:
        image: redis:latest
        ports:
          - "6379:6379"

      azure-vote-backend:
        image: mcr.microsoft.com/azuredocs/azure-vote-backend:v1
        environment:
          - REDIS=redis

      azure-vote-front:
        image: mcr.microsoft.com/azuredocs/azure-vote-front:v1
        ports:
          - "80:80"
    ```

## Deployment Steps

1. **Login to Azure:**

    ```sh
    docker login azure
    ```

2. **Create a Docker context for ACI:**

    ```sh
    docker context create aci myacicontext
    ```

    During this step, you will be prompted to select your Azure subscription and resource group.

3. **List Docker contexts to verify the new context:**

    ```sh
    docker context ls
    ```

4. **Use the new Docker context:**

    ```sh
    docker context use myacicontext
    ```

5. **Deploy the application using Docker Compose:**

    ```sh
    docker compose up
    ```

    This command will deploy the services defined in your `docker-compose.yaml` file to Azure Container Instances.

6. **Browse the Azure Container Instance:**

    Once the deployment is complete, get the IP address of the Azure Container Instance:

    ```sh
    docker ps
    ```

    Open a web browser and navigate to the IP address of the Azure Container Instance to access the Azure Vote app.

## Troubleshooting

- If you encounter any issues during the deployment, ensure you have the correct permissions and configurations in your Azure account.
- Verify the status of your Azure Container Instances through the Azure Portal or using the Azure CLI.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgements

- The Azure Vote app is provided by Microsoft as part of their documentation and tutorials.

---

Happy coding!
# Azure-Vote-App
