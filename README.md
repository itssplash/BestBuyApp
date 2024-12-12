# Best Buy Cloud-Native App Project

## 1. Updated Application Architecture
### Architecture Diagram
![image](https://github.com/user-attachments/assets/7eda2863-1823-4001-848c-28fdf99c430c)


### Application and Architecture Explanation
The application is a cloud-native microservices solution designed for Best Buy’s online store. The architecture is based on the design principles of the Algonquin Pet Store (On Steroids) with a key modification to use a managed service for the Order Queue (e.g., Azure Service Bus). This architecture allows scalable, independent, and loosely-coupled microservices to run seamlessly in a Kubernetes cluster.

**Core Components:**
- **Store-Front**: A customer-facing app for browsing products and placing orders.
- **Store-Admin**: An employee-facing app for managing products and viewing orders.
- **Order-Service**: Manages order creation and communicates with the managed order queue.
- **Product-Service**: Handles CRUD operations for product data.
- **Makeline-Service**: Processes and completes orders by reading from the order queue.
- **AI-Service**: Uses GPT-4 and DALL-E for generating product descriptions and images.
- **Database**: MongoDB for persisting data related to products and orders.

## 2. Deployment Instructions
### Prerequisites
- Kubernetes cluster (e.g., AKS)
- Docker for building images
- Access to Azure OpenAI Service or OpenAI APIs

### Deployment Steps
## 1. Clone this repository:
   ```bash
   git clone https://github.com/itssplash/BestBuyApp
   cd BestBuyApp
   ```
   
## 2. Deployment Instructions
### Prerequisites
- Kubernetes cluster (e.g., AKS)
- Docker for building images
- Access to Azure OpenAI Service or OpenAI APIs

### Deployment Steps
1. **Set up Docker images**: Build and push the Docker images for each microservice to Docker Hub:
    ```bash
    docker build -t <your-dockerhub-username>/<service-name>:<tag> .
    docker push <your-dockerhub-username>/<service-name>:<tag>
    ```
2. **Configure Kubernetes resources**: Ensure `kubectl` is configured and connected to your cluster. Apply the Kubernetes YAML deployment files:
    ```bash
    kubectl apply -f Deployment-Files/
    ```

3. **Deploy MongoDB StatefulSet**: Use `statefulset-mongodb.yaml` from the Deployment Files folder.

4. **Verify Deployment**: Check the status of your pods and services:
    ```bash
    kubectl get pods
    kubectl get services
    ```

## 3. Table of Microservice Repositories
| Service           | Repository Link               |
|-------------------|--------------------------------|
| Best Buy-Front       | https://github.com/itssplash/best-buy-front          |
| Best-Buy-Orders    | https://github.com/itssplash/best-buy-orders        |
| Best-Buy-Products   | https://github.com/itssplash/best-buy-products            |
| Best-Buy-Makeline | https://github.com/itssplash/best-buy-makeline          |
| Best-Buy-AIService        | https://github.com/itssplash/best-buy-aiservice                |
| Best-Buy-Admin       | https://github.com/itssplash/best-buy-admin   |
| Virtual-customer(optional)  | https://github.com/itssplash/virtual-customer-bestbuy |
| Virtual-worker(optional)  | https://github.com/itssplash/virtual-worker-bestbuy                              |

## 4. Table of Docker Images
| Service           | Docker Image Link             |
|-------------------|--------------------------------|
| Best Buy-Front      | https://hub.docker.com/repository/docker/itssplash/best-buy-front            |
| Best-Buy-Orders     | https://hub.docker.com/repository/docker/itssplash/best-buy-orders              |
| Best-Buy-Products    | https://hub.docker.com/repository/docker/itssplash/best-buy-products         |
| Best-Buy-Makeline  | https://hub.docker.com/repository/docker/itssplash/best-buy-makeline             |
| Best-Buy-AIService        | https://hub.docker.com/repository/docker/itssplash/best-buy-aiservice        |
| Best-Buy-Admin      | https://hub.docker.com/repository/docker/itssplash/best-buy-admin                     |
| Virtual-customer  | https://hub.docker.com/repository/docker/itssplash/virtual-customer-l8/general            |
| Virtual-worker    | https://hub.docker.com/repository/docker/itssplash/virtual-worker-l8/general                      |

## 5. Demo Video
Watch the demo video showcasing the application functionality, including AI-powered product descriptions and image generation, and the integration with the managed order queue service: [[Demo Video Link]](https://algonquinlivecom-my.sharepoint.com/:v:/g/personal/abhi0012_algonquinlive_com/EazYQaGhYMpEnriSo1_tK7YBFjX2e3Jsr30mNRWp-cix2w?e=Zt6OVM&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D)


### CI/CD Pipeline Implementation (Bonus)
- I have implemented a CI/CD pipeline for each microservice.
- You can check the Actions tab in the GitHub repository for each service or review the
ci_cd.yaml workflow file in the respective repository.

## 6. Known Issues and Limitations
1. **Connecting Order-Service with RabbitMQ**:  
   Establishing a seamless connection between the Order-Service and RabbitMQ required troubleshooting authentication and connection settings. Ensuring message delivery reliability was also a significant task, especially during high workloads.

2. **Integrating Makeline-Service with RabbitMQ**:  
   The Makeline-Service faced issues processing messages from RabbitMQ due to configuration mismatches and handling message retries for failed deliveries. Debugging these issues consumed additional time during development.

3. **AI Integration**:  
   - Integrating GPT-4 and DALL-E with the Azure OpenAI Service required managing API keys securely and ensuring that API quotas and limits were not exceeded during testing.  
   - Generating product descriptions and images for a large dataset demanded efficient use of resources and rate-limiting strategies.

4. **Kubernetes Deployment**:  
   Deploying the application on Kubernetes was complex due to the need to configure multiple microservices, StatefulSets, ConfigMaps, and Secrets. Ensuring communication between services within the cluster required careful setup of networking rules and service discovery.

5. **Handling Secrets and Sensitive Data**:  
   Managing sensitive information like API keys, database credentials, and RabbitMQ connection details securely using Kubernetes Secrets required thorough attention to detail to prevent unintentional leaks.

6. **Service Reliability in Kubernetes**:  
   - Encountered challenges in scaling services while maintaining consistent performance across multiple replicas.  
   - Implementing health checks for services to ensure self-healing in the event of a failure required additional testing and configuration.

7. **CI/CD Pipeline Setup (Optional Task)**:  
   - Automating builds and deployments for each microservice introduced complexity in managing pipeline configurations.  
   - Debugging failed builds or deployments in the CI/CD workflow required significant effort, especially for Kubernetes deployment steps.

### Known Limitations
- The application’s current implementation is dependent on Azure OpenAI Service or OpenAI APIs, which might incur additional costs or encounter rate limits during heavy usage.  
- RabbitMQ is used as a fallback for Azure Service Bus; however, this may not fully replicate the scalability and management features offered by a cloud-managed service.  
- MongoDB StatefulSet might face challenges during high scalability requirements due to its design limitations in Kubernetes.

## 7. Additional Notes
- Ensure you have configured your application with ConfigMaps and Secrets to manage configurations securely.
- The `AI-Service` utilizes the Azure OpenAI Service to interface with GPT-4 and DALL-E for generating AI-based content.
