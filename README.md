## Terraform Cluster Web Server with Load Balancing on AWS

This project demonstrates deploying a highly available cluster of web servers on Amazon Web Services (AWS) using Terraform. It leverages EC2 instances with Auto Scaling for scalability and an Elastic Load Balancer (ELB) for distributing traffic across the servers.

**Features:**

* **Automated Infrastructure Provisioning:** Terraform automates the creation and management of all infrastructure resources on AWS.
* **Scalable Web Server Cluster:** Auto Scaling ensures your application can handle varying traffic loads by automatically adding or removing web server instances.
* **Load Balancing:** The ELB distributes incoming traffic across healthy web servers in the cluster, ensuring high availability for your application.
* **Customizable Configuration:** You can easily modify server port, instance type, and other settings through Terraform variables.

**Requirements:**

* **Terraform:** [https://www.terraform.io/](https://www.terraform.io/) (version 0.10.x or later recommended)
* **AWS Account:** [https://aws.amazon.com/](https://aws.amazon.com/) with IAM user credentials configured

**Getting Started:**

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/Jenish2911/terraform-load-balancer
   cd terraform-load-balancer
   ```

2. **Configure AWS Credentials:**

   For security reasons, it's highly recommended to use IAM users with appropriate permissions instead of the root account for interacting with AWS resources. You can configure your credentials in one of the following ways:

      * **AWS Credentials File:**

         Create a file named `~/.aws/credentials` on Linux/macOS/Unix or `C:\Users\USERNAME\.aws\credentials` on Windows with the following format:

         ```
         [default]
         aws_access_key_id = <your_access_key_id>
         aws_secret_access_key = <your_secret_access_key>
         ```

         Replace `<your-access_key_id>` and `<your-secret_access_key>` with your actual credentials.

      * **Environment Variables:**

         Set the environment variables `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` with your credentials.

3. **Initialize Terraform:**

   Run the following command to initialize the Terraform working directory and download required plugins:

   ```bash
   terraform init
   ```

4. **Review and Customize Configuration:**

   The Terraform configuration files (`main.tf`, `vars.tf`) define the infrastructure resources to be deployed. You can review these files to understand the components and customize settings like:

      * **Server Port:** Edit the `server_port` variable in `vars.tf` to change the port on which web servers listen for requests (default: 8080).
      * **Instance Type:** Modify the `ami`, `region` and `instance_type` variables in `main.tf` to choose a different Amazon Machine Image (AMI), region in which you are working and instance type for your web servers.
      * **Security Groups:** Review and adjust security group rules in `main.tf` to control inbound and outbound traffic for your web servers and ELB.

5. **Validate Terraform Configuration:**

   Run the following command to validate the Terraform configuration and preview the planned infrastructure changes:

   ```bash
   terraform plan
   ```

   Carefully review the output to ensure the infrastructure will be created as intended.

6. **Deploy the Cluster:**

   Once you're satisfied with the planned changes, run the following command to deploy the infrastructure on AWS:

   ```bash
   terraform apply
   ```

   This will create the web server cluster, launch Auto Scaling group, and provision the ELB.

7. **Test the Cluster:**

   After successful deployment, the Terraform output will display the public DNS name of the ELB. Use this DNS name to access your web servers in a browser:

   ```
   http://<elb_dns_name>/
   ```

   You should receive a "Hello, World" response if everything is functioning correctly.

8. **Destroy the Cluster (Optional):**

   When you're finished with the cluster, run the following command to remove all resources created by Terraform:

   ```bash
   terraform destroy
   ```
   This will delete all the resources created by the terraform.

**Additional Notes:**

* This is a basic example for demonstration purposes. Real-world deployments might require additional security measures, logging configurations, and application-specific customizations.
* Consider exploring Terraform modules to achieve better code organization and reusability for complex deployments.
