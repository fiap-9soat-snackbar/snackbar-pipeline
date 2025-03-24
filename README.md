# CI/CD Pipeline

This repository contains the CI/CD pipeline configuration responsible for automating the build, test, and deploy processes of our Snackbar application. The pipeline has been configured to ensure the application is correctly tested and efficiently deployed using AWS Cloud and MongoDB Atlas infrastructure.

## Purpose

The main objective of this pipeline is to automate the following steps:

- **Build**: Create consistent builds to ensure the application is ready for execution.
- **Tests**: Run unit tests to validate the functionality of the code.
- **Deploy**: Automatically deploy the application to a cloud environment using tools like Terraform, Helm, and Kubernetes.

## Features

- **Application Build**: Generates the latest version of the application.
- **Test Execution**: Ensures the functionalities are working correctly before deployment.
- **Automated Deployment**: Deploys the application to the cloud environment.
- **Automated Infrastructure Provisioning**: Deploys the necessary infrastructure for the application to run, such as Kubernetes, API Gateway, Lambda Functions, and MongoDB.

## AWS Environment Variables

- **`AWS_ACCESS_KEY_ID`**: The programmatic access key ID for the AWS account, used for authentication when provisioning AWS resources.
- **`AWS_SECRET_ACCESS_KEY`**: The secret key associated with `AWS_ACCESS_KEY_ID`, used for secure authentication with AWS.
- **`AWS_SESSION_TOKEN`**: Temporary session token used for AWS authentication in secure access scenarios (typically generated when using IAM roles or MFA).
- **`AWS_DEFAULT_REGION`**: The AWS region where services like EC2, S3, and EKS will be provisioned (example: `us-east-1`).

## MongoDB Atlas Environment Variables

- **`MONGODBATLAS_ORG_PRIVATE_KEY`**: Private key for the MongoDB Atlas organization, used for authentication with MongoDB Atlas management APIs.
- **`MONGODBATLAS_ORG_PUBLIC_KEY`**: Public key for the MongoDB Atlas organization, used for authentication with MongoDB Atlas management APIs.
- **`ORG_ID`**: Unique ID of the MongoDB Atlas organization, used to reference the organization in scripts and automations.
- **`MONGO_HOST`**: The host (address) of the MongoDB cluster to be provisioned, used by the application to connect to the database.

## Docker Environment Variables

- **`DOCKER_USERNAME`**: Docker Hub username, used for authentication when logging in and pushing Docker images.
- **`DOCKER_PASSWORD`**: Password or access token for Docker Hub, used alongside `DOCKER_USERNAME` to log in to Docker Hub.

## JWT Environment Variables

- **`JWT_EXPIRES`**: Defines the expiration time of JWT tokens used by the application for authentication and authorization (usually in seconds).
- **`JWT_SECRET`**: Secret key used to sign and validate JWT tokens generated by the application.

## MongoDB Application Environment Variables

- **`MONGODBATLAS_USERNAME`**: Root username used to access the MongoDB Atlas cluster, configured for database authentication.
- **`MONGODBATLAS_PASSWORD`**: Password associated with `MONGODBATLAS_USERNAME`, used for MongoDB Atlas authentication.
- **`MONGODB_USER`**: MongoDB database username specific to the application, used to access the provisioned database.
- **`MONGO_APP_DB`**: The name of the database within MongoDB that the application will use (example: `snackbar`).

## Other Environment Variables

- **`SONAR_TOKEN`**: Token used for authentication with SonarQube, necessary for integrating and running code quality analysis.
- **`BUCKET_S3`**: Name of the S3 bucket in AWS used to store the `tfstate` file for infrastructure provisioning.

## Ensure that these environment variables are correctly configured for the pipeline to work properly.

## How to Use

To run the pipeline, ensure that all prerequisites are met, such as:

- Correctly configured AWS credentials.
- Correctly configured MongoDB Atlas credentials.
- The environment variables mentioned above are correctly set.

The pipeline will automatically run on every push or merge to the `main` branch of the following repositories:

- https://github.com/fiap-9soat-snackbar/snackbar - application repository
- https://github.com/fiap-9soat-snackbar/snackbar-lambda - lambda provisioning repository
- https://github.com/fiap-9soat-snackbar/snackbar-database - MongoDB Atlas provisioning repository
- https://github.com/fiap-9soat-snackbar/eks - Kubernetes provisioning repository using AWS EKS
- https://github.com/fiap-9soat-snackbar/snackbar-api-gateway - AWS API Gateway provisioning repository
