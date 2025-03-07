# **EC2 Automation with Terraform**

This guide provides step-by-step instructions to automate the provisioning of an **EC2 Instance** using **Terraform**.

---

## **1. Install Terraform**

- Download Terraform from the official [Terraform Download](https://www.terraform.io/) page.
- Verify the installation by running:

```bash
terraform -v
```

![Terraform Installation](https://github.com/user-attachments/assets/d57c1e31-f555-4ed0-8aef-fcb8709ef454)

---

## **2. Configure AWS Credentials**

Terraform requires AWS credentials to interact with AWS services. Set up your credentials by running:

```bash
aws configure
```

![AWS Credentials](https://github.com/user-attachments/assets/82263952-781f-42e1-9ea8-a2c27797248f)

---

## **3. Create a Terraform Configuration File**

- Create a directory for your Terraform project and navigate to it.
- Inside this directory, create a file named `main.tf`.

```bash
mkdir terraform-ec2 && cd terraform-ec2
touch main.tf
```

![Create main.tf](https://github.com/user-attachments/assets/13ef8614-9cd0-41ab-8bf2-96ad3927e5c8)

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

![Terraform Configuration](https://github.com/user-attachments/assets/67d56f09-7625-49a4-acb4-25e790e0f78e)

---

## **5. Initialize Terraform**

Run the following command to initialize Terraform:

```bash
terraform init
```

![Terraform Init](https://github.com/user-attachments/assets/d889bba6-c647-4f4e-8ce2-b1070f5e3324)

---

## **6. Validate and Plan Configuration**

- Validate the syntax and check what resources Terraform will create:

```bash
terraform validate
terraform plan
```

![Terraform Plan](https://github.com/user-attachments/assets/320856ef-395c-4056-b4c0-0fef93fd63d1)

---

## **7. Apply the Configuration**

- Deploy the EC2 instance by running:

```bash
terraform apply -auto-approve
```

![Terraform Apply](https://github.com/user-attachments/assets/988dcda5-8ef0-4241-a2e8-b585e04170f0)
![Instance Creation](https://github.com/user-attachments/assets/382bdb26-76ae-424c-8ba4-10d77f817786)

---

## **8. Verify the Instance**

- After creation, verify the instance status by running:

```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]' --output table
```

![Verify Instance](https://github.com/user-attachments/assets/d2497593-6c30-45c2-8761-fd6c2b2dc4fc)

- Alternatively, check the instance in the AWS Console.

![AWS Console](https://github.com/user-attachments/assets/10f02230-fde0-4f5f-951e-92cfc2ae3c29)

---

## **9. Destroy the Instance**

- To remove the EC2 instance, run:

```bash
terraform destroy -auto-approve
```

![Terraform Destroy](https://github.com/user-attachments/assets/2497b0cf-2584-457f-aa2d-baf637e7bc7e)
![Instance Deletion](https://github.com/user-attachments/assets/1e670c1e-c003-47b5-a173-e62ed99381e9)

---

## **10. Conclusion**

Congratulations! You have successfully automated the provisioning and management of an **EC2 instance** using **Terraform**. This setup allows you to efficiently create and destroy instances without using the AWS Console.

For more advanced configurations, refer to the [Devstack Documentation](https://github.com/openstack/devstack).

