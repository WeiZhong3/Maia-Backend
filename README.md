# Maia Backend

This repository contains the backend code for Maia Project. It includes APIs, database models, and infrastructure setup using Terraform.

## Table of Content
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [API Documentation](#api-documentation)

### Prerequisites
- Amazon Web Service (AWS) Account
- Python 
- Terraform
- Docker


### Setup
1. Clone the repository
```
git clone https://github.com/WeiZhong3/Maia-Backend.git
```
2. Install dependencies
```
pip install -r requirements.txt
```
3. Setup AWS infrastructure using Terraform
    - Change working directory to `terraform`
    ```
    cd terraform
    ```

    - Create a terraform.tfvars file in the root directory and add your environment-specific variables
        - **`access_key`**: 
            - **Description**: The AWS Access Key ID used for authenticating with AWS services. This key is part of your AWS credentials and is required for Terraform to create and manage resources in your AWS account.
            - **Type**: `str`

        - **`secret_key`**: 
            - **Description**: The AWS Secret Access Key associated with the AWS Access Key ID. This secret key is used alongside the Access Key ID to authenticate with AWS services securely.
            - **Type**: `str`

        - **`region`**: 
            - **Description**: The AWS region where your resources will be provisioned. AWS regions are geographic locations that host AWS data centers, and this variable specifies which region your Terraform configuration should target.
            - **Type**: `str`

        - **`vpc_id`**: 
            - **Description**: The ID of the Virtual Private Cloud (VPC) in which your resources will be deployed. A VPC is a virtual network dedicated to your AWS account, providing isolation and security for your resources.
            - **Type**: `str`

        - **`db_username`**: 
            - **Description**: The username for accessing the database. This is used for authenticating with the database instance that Terraform provisions.
            - **Type**: `str`

        - **`db_password`**: 
            - **Description**: The password associated with the `db_username`. This password is used to authenticate with the database instance securely.
            - **Type**: `str`

        - **`opensearch_username`**: 
            - **Description**: The username for accessing the OpenSearch service (or Elasticsearch). This is used for authentication and managing access to the OpenSearch cluster.
            - **Type**: `str`

        - **`opensearch_password`**: 
            - **Description**: The password associated with the `opensearch_username`. This password is used to authenticate with the OpenSearch service securely.
            - **Type**: `str`

        - **`account_id`**: 
            - **Description**: The AWS account ID where the resources will be created. This ID uniquely identifies your AWS account and is often used in IAM policies and resource configurations.
            - **Type**: `str`

    - Initialise Terraform
    ```
    terraform init
    ```

    - Plan the deployment
    ```
    terraform plan
    ```

    - Apply the configuration
    ```
    terraform apply
    ```

4. Apply database migrations
```
python manage.py migrate
```

5. Configure environment variables in a `.env` file in root directory.
    - **`OPENAI_API_KEY`**:
        - **Description**: The API key for accessing OpenAI services. This key is used to authenticate requests to the OpenAI API.
        - **Type**: `str`

    - **`DB_NAME`**:
        - **Description**: The name of the AWS RDS database used by the application. This is the database where the application's data will be stored.
        - **Type**: `str`

    - **`DB_USER`**:
        - **Description**: The username for connecting to the AWS RDS database. This user is used to authenticate access to the database.
        - **Type**: `str`

    - **`DB_PASSWORD`**:
        - **Description**: The password associated with the `DB_USER`. This password is used to securely authenticate the connection to the AWS RDS database.
        - **Type**: `str`

    - **`DB_HOST`**:
        - **Description**: The hostname or IP address of the AWS RDS database server. This specifies where the database server is located.
        - **Type**: `str`

    - **`DB_PORT`**:
        - **Description**: The port number on which the AWS RDS database server is listening. This is used to connect to the database service.
        - **Type**: `int`

    - **`OPENSEARCH_USERNAME`**:
        - **Description**: The username for accessing the AWS OpenSearch service. This is used for authentication and managing access to the OpenSearch cluster.
        - **Type**: `str`

    - **`OPENSEARCH_PASSWORD`**:
        - **Description**: The password associated with the `OPENSEARCH_USERNAME`. This password is used to authenticate with the OpenSearch service securely.
        - **Type**: `str`

    - **`AWS_ACCESS_KEY_ID`**:
        - **Description**: The AWS Access Key ID used for authenticating with AWS services. This key is part of your AWS credentials and is required for AWS service access.
        - **Type**: `str`

    - **`AWS_SECRET_ACCESS_KEY`**:
        - **Description**: The AWS Secret Access Key associated with the AWS Access Key ID. This secret key is used alongside the Access Key ID to securely authenticate with AWS services.
        - **Type**: `str`

6. Run the server
```
uvicorn backend.asgi:application --host 127.0.0.1 --port 8000
```

## API Documentation
The API documentation is available through Swagger. To view it:

1. Start the Server (make sure the backend is running as described above).

2. Navigate to the Swagger UI
    - Open your browser and go to:
    ```
    http://localhost:8000/swagger/
    ```
    > **Note**: Replace `8000` with your server port if it is different from the default port.