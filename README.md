# aws-challenge-week-6-part-1
Week 6 of the 12 weeks of AWS challenge

This week focused on infrastructure as code, specifically CloudFormation. Cloudformation allows you to model your infrastucture in a text file, using JSON or YAML to describe what AWS resources you want to create and configure. Cloudformation automates the provisioning and updating of your infrastructure in a safe and controlled manner, there are no manual steps or controls that can lead to errors. 

## Template and Stack
An AWS CloudFormation template is a declaration of the AWS resources that make up a stack. The template is stored as a text file in either JSON or YAML format. 
A stack is a deployment of a CloudFormation template. A stack contains a collection of multiple AWS resources that you can manage as a single unit. All resources in a stack are defined by the stack's AWS CloudFormation template. 

In the hands on lab, I will be doing the following: 
* Write a CloudFormation template that describes an S3 bucket
* Deploy the template and create a CloudFormation stack

1. Add the code that creates an S3 bucket to the template-and-stack.yaml file

<img width="598" alt="4" src="https://github.com/user-attachments/assets/2ac31745-7285-43a8-8ecc-a60dbe6845df" />

2. Create a stack using the Cloudformation template (template-and-stack.yaml) that was created in the previous step

<img width="954" alt="5" src="https://github.com/user-attachments/assets/b477573c-1c73-4709-9891-5396ac6d5db9" />

3. The S3 bucket that was created using CloudFormation

<img width="953" alt="6" src="https://github.com/user-attachments/assets/6f4e7531-7513-4d0f-9c15-72f6f506dfa6" />

4. Modify the template to enable versioning on the S3 bucket to prevent objects from being deleted or overwritten

<img width="303" alt="7" src="https://github.com/user-attachments/assets/5db1e7da-51f1-449f-9951-4dbf2de41e4d" />

5. Update the stack on CloudFormation with to use the modified template

<img width="956" alt="8" src="https://github.com/user-attachments/assets/defc0747-4bdd-438b-81ab-9ed309378ea9" />

6. Verfiy that versioning is enabled on the S3 bucket

<img width="696" alt="9" src="https://github.com/user-attachments/assets/2e333dee-f331-40d2-a1d7-45d1b379be1a" />

7. Clean up resources by deleting the stack

## Reasources
The required Resources section declares the AWS resources that you want to include in the stack

In the hands on lab, I will be doing the following: 
* Deploy an Ec2 instance via CloudFormation

1. Open the resources.yaml file and add the following to the template
* Format version
* Description
* Meta data
* Parameters
* Resources

<img width="350" alt="10" src="https://github.com/user-attachments/assets/4803002f-2fad-41fa-b31e-89f214603076" />

2. Create a stack using the Cloudformation template that was created in the previous step

<img width="953" alt="11" src="https://github.com/user-attachments/assets/2c1484a9-d742-4127-9464-77e9ea3254ff" />

3. Verify that the EC2 instance was successfully created

<img width="950" alt="12" src="https://github.com/user-attachments/assets/9b3bb71c-f21e-4406-84ef-7648d04ba284" />

4. Clean up resources by deleting the stack

## Intrinsic functions
Intrinsic functions are built-in function that help you manage your stacks. Without them, you will be limited to very basic templates. 

In the hands on lab, I will be doing the following:
* Use the Ref function to dynamically assign parameter values to a resource property
* Tag an instance with Fn::Join function
* Add a tag to the instance using Fn::Sub function

1. Add the following code to create a new parameter called **AmiID** in the intrinsic-functions.yaml template

<img width="241" alt="13" src="https://github.com/user-attachments/assets/af61cc0e-d021-40db-9573-db4019bad199" />

2. Use the intrinsic function **Ref** to pass the **AmiID** parameter input to the EC2 resource property

<img width="283" alt="14" src="https://github.com/user-attachments/assets/61681dae-4df8-4f02-a9f5-871535933c31" />

3. Add property **Tags** to the Properties section and reference **InstanceType** parameter, add *webserver*, delimited with a dash to the tags property

<img width="383" alt="15" src="https://github.com/user-attachments/assets/0be8fb6e-f1d4-4af0-a9cd-f60ad9c7f913" />

4. Create a stack using the CloudFormation template. The tags that were successfully created.

<img width="495" alt="16" src="https://github.com/user-attachments/assets/db00855d-c5d9-4179-ba93-8580ed32f96a" />

5. Clean up resources by deleting the stack.







