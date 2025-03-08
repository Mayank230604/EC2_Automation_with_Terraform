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
![image](https://github.com/user-attachments/assets/d29ed685-2c4c-4397-9713-1220c6b9aefe)

---

## **4. Define the EC2 Instance in Terraform**

- Open `main.tf` and add the following Terraform configuration:

```hcl
provider "aws" {
    profile = "default"
    region  = "eu-west-2"
}

resource "aws_instance" "UGO_Server" {
    ami           = "ami-0cbf43fd299e3a464"
    instance_type = "t2.micro"

    tags = {
        Name = "MyNCAAInstance"
    }
}
```
![image](https://github.com/user-attachments/assets/398be90b-7c90-456a-8042-605dffae01ac)


---

## **5. Initialize Terraform**

Run the following command to initialize Terraform:

```bash
terraform init
```
![image](https://github.com/user-attachments/assets/4c04a20d-a71a-4368-b6e1-139673e8ff27)

---

## **6. Validate and Plan Configuration**

- Validate the syntax and check what resources Terraform will create:

```bash
terraform validate
terraform plan
```
![image](https://github.com/user-attachments/assets/c1209480-64fb-4aa2-9591-21c7e25cb373)

---

## **7. Apply the Configuration**

- Deploy the EC2 instance by running:

```bash
terraform apply -auto-approve
```
![image](https://github.com/user-attachments/assets/808936ce-36b2-475a-b921-f7252078fee1)
![image](https://github.com/user-attachments/assets/5c1a2928-999e-4786-bd84-0bd02bf9ab57)

---

## **8. Verify the Instance**

- After creation, verify the instance status by running:

```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]' --output table
```
![image](https://github.com/user-attachments/assets/9b259335-5126-403d-a6ac-fc7bc906fa53)

- Alternatively, check the instance in the AWS Console.

![image](https://github.com/user-attachments/assets/72817dae-48e7-4097-86ff-2c65ad26aab9)

---

## **9. Destroy the Instance**

- To remove the EC2 instance, run:

```bash
terraform destroy -auto-approve
```
![image](https://github.com/user-attachments/assets/241ee758-0aaf-4aad-b311-1527999d7e77)
![image](https://github.com/user-attachments/assets/b9885ac3-a076-45f5-b140-4c2a44248442)

---

## **10. Conclusion**

Congratulations! You have successfully automated the provisioning and management of an **EC2 instance** using **Terraform**. This setup allows you to efficiently create and destroy instances without using the AWS Console.

For more advanced configurations, refer to the [Devstack Documentation](https://github.com/openstack/devstack).

