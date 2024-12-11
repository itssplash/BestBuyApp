# Best Buy Cloud-Native App Project

## 1. Updated Application Architecture
### Architecture Diagram
*Include the updated architecture diagram here. You can use Draw.io or a similar tool to create and embed the diagram.*

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
1. **Clone this repository**:
   ```bash
   git clone <repository-link>
   cd <repository-folder>
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
| Store-Front       | [GitHub Link]                 |
| Order-Service     | [GitHub Link]                 |
| Product-Service   | [GitHub Link]                 |
| Makeline-Service  | [GitHub Link]                 |
| AI-Service        | [GitHub Link]                 |

## 4. Table of Docker Images
| Service           | Docker Image Link             |
|-------------------|--------------------------------|
| Store-Front       | [Docker Hub Link]             |
| Order-Service     | [Docker Hub Link]             |
| Product-Service   | [Docker Hub Link]             |
| Makeline-Service  | [Docker Hub Link]             |
| AI-Service        | [Docker Hub Link]             |

## 5. Demo Video
Watch the demo video showcasing the application functionality, including AI-powered product descriptions and image generation, and the integration with the managed order queue service: [Demo Video Link]

## 6. Optional Task: CI/CD Pipeline
*Note: The professor has mentioned that RabbitMQ should be used if Azure Service Bus is not functional. Implementing the optional CI/CD task will result in full marks for the assignment.*

### CI/CD Pipeline Implementation (Bonus)
- Set up a CI/CD pipeline for each microservice using GitHub Actions or Azure DevOps.
- Automate the build, test, and deployment processes to ensure continuous integration and continuous deployment.

## 7. Known Issues and Limitations (Optional)
*List any issues or limitations you encountered during development.*

## 8. Additional Notes
- Ensure you have configured your application with ConfigMaps and Secrets to manage configurations securely.
- The `AI-Service` utilizes the Azure OpenAI Service to interface with GPT-4 and DALL-E for generating AI-based content.
