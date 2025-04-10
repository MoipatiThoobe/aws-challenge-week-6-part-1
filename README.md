<img width="679" alt="17" src="https://github.com/user-attachments/assets/de25d801-1c74-4d3b-824c-ce1c7beb52d3" /># aws-challenge-week-6-part-1
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


## Pseudo parameters
Pseudo parameters are parameters predefined by CloudFormation. You can use a pseudo parameter the same way you use a parameter.

In the hands on lab, I will be doing the following: 
* Leveraging pseudo parameters for template portability best practices
* Identify sample use cases for leveraging pseudo paramaters

1. Open the pseudo-parameters.yaml file and define a template parameter called *DatabaseUsername* in the Parameters section

<img width="679" alt="17" src="https://github.com/user-attachments/assets/faac87d6-3b4a-4919-a3c3-768afebc7b2d" />

2. Add the following code that describes the SSM parameter to the file

<img width="223" alt="17 1" src="https://github.com/user-attachments/assets/fc855b7b-a81c-4800-a96b-5cd46d2f9cb9" />

3. Add the following code that references the SSM parameter that was previously defined

<img width="676" alt="18" src="https://github.com/user-attachments/assets/117d1c8d-9a93-4aaf-b696-f132c6ff312d" />

4. Replace the code in the Policies section with the following

<img width="401" alt="18 1" src="https://github.com/user-attachments/assets/77506f7d-a127-4a2e-8d6d-b65c882e6c03" />

5. Add the following code that defines a Lambda function that uses the IAM Role that was defined above with permissions to read the SSM parameter

<img width="502" alt="19" src="https://github.com/user-attachments/assets/d2879114-23b9-45a9-8dc1-a88bf28a77c3" />

6. Create a stack using the CloudFormation template

<img width="956" alt="20" src="https://github.com/user-attachments/assets/1e3a5fc2-1933-4035-b2a4-091c5a4176b1" />

7. New resources are created and are shown in the Resources tab of the CloudFormation stack console

<img width="308" alt="21" src="https://github.com/user-attachments/assets/7d5da3df-e3b0-47ea-a67e-2d829be0302b" />

8. Verify the IAM permission that were described in the template

<img width="707" alt="22" src="https://github.com/user-attachments/assets/1a9caf4a-62d3-4ccf-b267-a0d892cebbed" />

<img width="416" alt="23" src="https://github.com/user-attachments/assets/8705211b-2863-43ea-8424-3f3ff8354eaa" />

9. Verify that the Lambda function has the permissions to access the SSM parameter by manually invoking the Lambda function

<img width="953" alt="24" src="https://github.com/user-attachments/assets/3c7604d4-3596-410a-b7c9-96871d08715e" />

10. Clean up resources by deleting the stack

## Mappings
A mappings section is a top level section of a CloudFormation template. It is used to define maps, their keys and values which can be then referenced in the template. 

In the hands on lab, I will be doing the following:
* Creating a mapping for environment type. Each environment type will be mapped to a different instance type.
* Finding the required value in mappings and reference it in properties section of the EC2 resource

1. Open the mappings.yaml file, in the *Parameters* section replace the *InstanceType* with the following code.
 
<img width="412" alt="25" src="https://github.com/user-attachments/assets/f05d2bde-1677-434b-afe8-b148ab13ba98" />

2. Create *EnvironmentToInstanceType* in the mappings section

<img width="299" alt="27" src="https://github.com/user-attachments/assets/7dcd5cb2-5bbd-4907-b523-1f03fc39dcfc" />

3. Modify the *InstanceType* property

<img width="310" alt="28" src="https://github.com/user-attachments/assets/c8e23e43-d662-4a76-b46a-bef062650f2b" />

4. Update the Tags property

<img width="319" alt="29" src="https://github.com/user-attachments/assets/5b5d8f84-bbc1-48df-abaa-b1b0f96f1e63" />

5. Create a stack using the CloudFormation template

<img width="952" alt="30" src="https://github.com/user-attachments/assets/675a0c56-68c4-479a-b9b6-5cb79d0e96b4" />

6. Clean up resources by deleting the stack

## Outputs
Outputs enable you to get access to information about resources within a stack. Furthermore, output values can be imported into other stacks, these are known as cross-stack references. 

In the hands on lab, I will be doing the following:
* Creating an Output section in the template and return the Public DNS name of the instance
* Learn how to view outputs from within CloudFormation in the AWS console

1. Open outputs.yaml file and add the following code to get the Public DNS name of the instance

<img width="341" alt="31" src="https://github.com/user-attachments/assets/f37d861c-0fa1-44db-aa25-f818defb6d0a" />

2. Create a stack using the CloudFormation template

<img width="950" alt="32" src="https://github.com/user-attachments/assets/0cccd487-9a20-4546-a8d5-1df20ea83080" />

3. View the output value in the Outputs tab of the CloudFormation console

<img width="438" alt="33" src="https://github.com/user-attachments/assets/1b491efa-8ef0-4381-ae50-bf544575cbb5" />

4. Clean up resources by deleting the stack


## Finding return values
Return values are documented in the AWS resource and property types reference for a given resource type, you can choose any resource type from the list and then choose **Return values** on the right side of the page to see which values you can use with intrinsice functions. 

In the hands on lab, I will be doing the following:
* Utilizing return values of a resource in other resources described in the same template
* Define stack outputs based on the resource return values using intrinsic functions

1. Open the resource-return-values.yaml and add the following code

<img width="185" alt="34 1" src="https://github.com/user-attachments/assets/a32335fc-4d86-4f2a-afc4-934af42adcc3" />

2. Create a stack using the resource-return-values.yaml template

<img width="956" alt="34" src="https://github.com/user-attachments/assets/53d868e4-152b-4f48-952d-2de48e813a31" />

3. View the resources that were created in the Resource tab of CloudFormation

<img width="439" alt="35" src="https://github.com/user-attachments/assets/335dd02d-046b-4f2d-ac3f-30c59158b83a" />

4. The bucket policy that was created

<img width="440" alt="36" src="https://github.com/user-attachments/assets/c8274ad3-6303-444d-820f-0ea95dfd5089" />

5. View the bucket domain name in the Outputs tab of the CloudFormation console

<img width="451" alt="37" src="https://github.com/user-attachments/assets/b6b6c4ef-5616-4a63-92c4-1a2ce37cf467" />

6. Clean up resources by deleting the stack




