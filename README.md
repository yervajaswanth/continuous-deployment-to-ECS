# AWS Infrastructure Setup with Terraform and Deployment Workflows

This repository contains Terraform configurations for setting up AWS infrastructure and GitHub Actions workflows for deploying applications to Amazon ECS (Elastic Container Service).

## Setup Instructions

### Terraform Setup

1. **Clone the Repository**: Clone this repository to your local machine.

    ```bash
    git clone https://github.com/your-username/your-repo.git
    ```

2. **Install Terraform**: Install Terraform on your local machine. You can download Terraform from the [official website](https://www.terraform.io/downloads.html) and follow the installation instructions.

3. **Set up AWS Credentials**: Ensure you have AWS credentials configured on your local machine. You can set up AWS credentials using the AWS CLI or by directly editing the `~/.aws/credentials` file.

### Infrastructure Deployment with Terraform

1. **Navigate to the Terraform Directory**: Go to the `terraform` directory in the cloned repository.

    ```bash
    cd terraform
    ```

2. **Initialize Terraform**: Run `terraform init` to initialize Terraform and download the required plugins.

    ```bash
    terraform init
    ```

3. **Review Terraform Plan**: Run `terraform plan` to see the execution plan and verify what resources will be created.

    ```bash
    terraform plan
    ```

4. **Apply Terraform Changes**: If the plan looks good, apply the changes using `terraform apply`.

    ```bash
    terraform apply
    ```

    You will be prompted to confirm the changes. Type `yes` to apply the changes and create the infrastructure.

### Deployment Workflows with GitHub Actions

1. **Enable GitHub Actions**: Ensure GitHub Actions is enabled for your repository.

2. **Add AWS Credentials to Secrets**: Go to your repository settings on GitHub and navigate to the "Secrets" section. Add your AWS access key ID and secret access key as secrets with appropriate names.

3. **Configure Workflow Environment Variables**: Update the environment variables in the `.github/workflows/deploy.yml` file according to your AWS setup.

4. **Commit and Push Changes**: Commit and push the changes to trigger the deployment workflow.

## Mechanism of Deployment Workflow

The deployment workflow (`deploy.yml`) uses GitHub Actions to automate the deployment process. Here's how it works:

- **Event Trigger**: The workflow is triggered on every push to the `main` branch of the repository.

- **Environment Setup**: It sets up the required environment variables, including AWS region, ECR repository name, ECS service name, ECS cluster name, task definition file path, and container name.

- **Steps Execution**: The workflow consists of several steps:

  - **Checkout**: It checks out the repository code.
  
  - **Configure AWS Credentials**: It configures AWS credentials using the provided secrets.
  
  - **Login to Amazon ECR**: It logs in to Amazon ECR using the AWS credentials.
  
  - **Build and Push Image**: It builds the Docker image, tags it, and pushes it to Amazon ECR.
  
  - **Update Task Definition**: It updates the ECS task definition with the new Docker image.
  
  - **Deploy Task Definition**: It deploys the updated task definition to the ECS service.
  
By following this workflow, you can automate the deployment of your application to Amazon ECS whenever changes are pushed to the `main` branch of your repository.
