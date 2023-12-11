# EKS Deployment

# Architecture
![architecture](https://github.com/Jainsi1/K8s-Deplyment/assets/75137939/201bb01c-f6ac-4388-a0dc-6d410ec330fe)


# Features
* Contains a bash file in which terraform commands are written to build infrastructure and it also installs all the required helm charts.
* For doing this complete setup you have to just run the bash file by giving it permission to execute as:

  1. chmod +x main.sh
  2. ./main.sh

# HelmCharts 
 Helm charts used here are as:

1. ## Nginx Ingress Controller:
NGINX Ingress Controller provides a robust feature set to secure, strengthen, and scale your containerized apps.
NGINX Ingress Controller works with both NGINX and NGINX Plus and supports the standard Ingress features - content-based routing and TLS/SSL termination. NGINX Ingress Controller supports the VirtualServer and VirtualServerRoute resources. They enable use cases not supported with the Ingress resource, such as traffic splitting and advanced content-based routing.
https://github.com/kubernetes/ingress-nginx


2. ## Cluster Autoscaler:
Kubernetes Cluster Autoscaler automatically adjusts the number of nodes in your cluster when pods fail or are rescheduled onto other nodes. The Cluster Autoscaler is typically installed as a Deployment in your cluster.
Cluster autoscaler scales down only the nodes that can be safely removed.
https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler

3. ## Secrets Store CSI Driver
The Secrets Store CSI Driver is used with AWS Secrets Manager to securely store and retrieve secrets within a Kubernetes cluster. It provides a seamless integration with AWS Secret Manager, allowing users to leverage its features for managing sensitive information such as API keys, database credentials, and certificates in their Kubernetes applications. This ensures a more secure and scalable approach to secret management in AWS environments.
https://secrets-store-csi-driver.sigs.k8s.io/

4. ## Secrets Store CSI Driver Provider AWS
The Secrets Store CSI Driver Provider AWS is used with the Secrets Store CSI Driver to enable seamless integration with AWS services, specifically AWS Secrets Manager. It acts as a bridge between the Secrets Store CSI Driver and AWS Secrets Manager, allowing Kubernetes applications to securely access and manage secrets stored in AWS Secrets Manager.
https://github.com/aws/secrets-store-csi-driver-provider-aws


# Inputs

|Name              |Description                                          |Type   |Default|
|------------------|-----------------------                              |-------|-------|
|vpc_name    |Name of your vpc                               |string |""     |
|vpc_cidr  |The IPv4 CIDR block for the VPC                    |string |0.0.0.0/0|
|vpc_azs          |A list of availability zones names                          |list(string) |[ ]     |
|vpc_private_subnets    |private subnets inside the VPC              |list(string) |[ ]       |
|vpc_public_subnets          |private subnets inside the VPC | list(string)  |[ ]  |
|vpc_tags |Additional tags for the VPC	        |map(string) |{ }     |
|eks_cluster_name    |Name of your cluster                               |string |""     |
|eks_cluster_version  | Kubernetes `<major>.<minor>` version to use for the EKS cluste       |string |null    |
|eks_managed_node_group_default_instance_type          |Instance types                          |string |""     |
|managed_nodes_min_capacity    |minimum  number of  pods running        |number |  1     |
|managed_nodes_max_capacity          |maximum number of  pods running |number   |  |
|managed_nodes_desired_capacity | desired size of pod which we want always|number |     |
|managed_nodes_instance_type_list    |    instance types      | list(string)|[ ]    |
|managed_nodes_capacity_type  | Capacity type of ec2          |string |On Demand     |
|managed_nodes_tags          |Aditional tags for the node |map(string) |{ }|


# Outputs

|Name              |Description                        |                                    
|------------------|-----------------------            |                
|eks_cluster_name    |Name that identifies the cluster |                   
|eks_cluster_arn       |ARN that identifies the cluster    |   
|eks_oidc|The URL on the EKS cluster for the OpenID Connect identity provider|
|eks_oidc_provider|The OpenID Connect identity provider|
|oidc_provider_arn|The ARN of the OIDC Provider|
|cluster-autosclaer-role-arn  |ARN of the cluster-autoscaler role|
|cluster-version|version of cluster|




**TASK2**:
Fetch Data from API and Write to CSV

#Description
This script retrieves data from a specified API endpoint and writes the fetched information to a CSV file. The data fetched from the API pertains to universities in Canada and includes fields such as 'Name', 'Country', 'Domain', and 'Web Page'. The script processes the JSON response received from the API and writes it into a CSV file, organizing each record according to the specified fields.

#Usage
API Endpoint: Ensure the api_url variable contains the correct URL to the API endpoint that provides university data. The provided endpoint should return a JSON response with university information.

CSV File: The script specifies a csv_filename variable as the output file. This file will be created/overwritten in the script's execution directory and named 'universities_canada.csv'.

Running the Script: Execute the script, providing the API endpoint URL and CSV filename as arguments to the fetch_data_to_csv function.

#Script Workflow:

1.Sends a GET request to the specified API endpoint.
2.Processes the JSON response, extracting relevant university data like name, country, domain, and web page.
3.Creates a CSV file and writes the extracted data into the file with appropriate headers.

#Note
API Endpoint: Ensure the API endpoint is accessible and provides the expected JSON response with university data.
The script assumes a single domain and web page for each university but can be modified if the API provides multiple values.
Double-check the CSV output to ensure the data is correctly formatted according to the specified headers.



**TASK3:**
Update Records via API from CSV

#Description:

This script facilitates updating or creating records in a system through a provided API endpoint using data from a CSV file. The script reads a CSV file containing university data and interacts with the specified API to update existing records or create new ones based on the information provided in the CSV.

#Usage
CSV File: Ensure the CSV file contains data in the specified format with columns such as 'Name', 'Country', 'Domain', and 'Web Page'. Modify the script as needed to match the actual structure of your CSV file.

#API Endpoint: Replace api_endpoint variable with the actual endpoint URL where the records need to be updated or created.

#Running the Script: Execute the script, providing the CSV file path and API endpoint as arguments to the update_records_via_api function.

#Script Workflow:
Reads data from the specified CSV file.

1.Processes each row of data from the CSV file, preparing a payload for interaction with the API.
2.Checks if the university already exists in the system via a GET request to the API.
3.If the university exists, attempts to update the existing record using a PUT or PATCH request.
4.If the university doesn't exist, creates a new record using a POST request to the API.

Note:
Review the API documentation to ensure compatibility with the provided data and operations (PUT, PATCH, POST).
Verify that the data in the CSV aligns with the expected format for interacting with the API.




