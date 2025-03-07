# **EC2 Automation with Terraform**

This guide provides step-by-step instructions to automate the provisioning of an **EC2 Instance** using **Terraform**.

---

## **1. Install Terraform**

- Download Terraform from the official [Terraform Download](https://www.terraform.io/) page.
- Verify the installation by running:

```bash
terraform -v
```
![image](https://github.com/user-attachments/assets/d91ef44b-234b-4378-88f7-bad3275f5011)

---

## **2. Configure AWS Credentials**

Terraform requires AWS credentials to interact with AWS services. Set up your credentials by running:

```bash
aws configure
```
![image](https://github.com/user-attachments/assets/e2f736ab-2f77-44ec-ba57-69df1395f24e)

---

## **3. Create a Terraform Configuration File**

- Create a directory for your Terraform project and navigate to it.
- Inside this directory, create a file named `main.tf`.

```bash
mkdir terraform-ec2 && cd terraform-ec2
touch main.tf
```

---

## **4. Define the EC2 Instance in Terraform**

- Open `main.tf` and add the following Terraform configuration:

```hcl
provider "aws" {
  region = "us-east-1"  # Modify as needed
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux AMI (Check for your region)
  instance_type = "t2.micro"

  tags = {
    Name = "MyTerraformInstance"
  }
}
```

---

## **5. Initialize Terraform**

Run the following command to initialize Terraform:

```bash
terraform init
```

---

## **6. Validate and Plan Configuration**

- Validate the syntax and check what resources Terraform will create:

```bash
terraform validate
terraform plan
```

---

## **7. Apply the Configuration**

- Deploy the EC2 instance by running:

```bash
terraform apply -auto-approve
```

---

## **8. Verify the Instance**

- After creation, verify the instance status by running:

```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]' --output table
```

- Alternatively, check the instance in the AWS Console.

---

## **9. Destroy the Instance**

- To remove the EC2 instance, run:

```bash
terraform destroy -auto-approve
```

---

## **10. Conclusion**

Congratulations! You have successfully automated the provisioning and management of an **EC2 instance** using **Terraform**. This setup allows you to efficiently create and destroy instances without using the AWS Console.

For more advanced configurations, refer to the [Devstack Documentation](https://github.com/openstack/devstack).

