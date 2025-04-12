# aws-challenge-week-6-part-1
Week 6 of the 12 weeks of AWS challenge

This week focused on infrastructure as code, specifically CloudFormation. Cloudformation allows you to model your infrastructure in a text file, using JSON or YAML to describe what AWS resources you want to create and configure. Cloudformation automates the provisioning and updating of your infrastructure in a safe and controlled manner, there are no manual steps or controls that can lead to errors. 

## Prerequisites
1. Clone the repository to your working directory to get the CloudFormation templates
```
git clone https://github.com/aws-samples/cfn101-workshop
```


## Template and Stack
An AWS CloudFormation template is a declaration of the AWS resources that make up a stack. The template is stored as a text file in either JSON or YAML format. 
A stack is a deployment of a CloudFormation template. A stack contains a collection of multiple AWS resources that you can manage as a single unit. All resources in a stack are defined by the stack's AWS CloudFormation template. 

In the hands on lab, I will be doing the following: 
* Write a CloudFormation template that describes an S3 bucket
* Deploy the template and create a CloudFormation stack

1. Open the template-and-stack.yaml file and add the following code to create an S3 bucket

<img width="598" alt="4" src="https://github.com/user-attachments/assets/2ac31745-7285-43a8-8ecc-a60dbe6845df" />

2. Create a stack on CloudFormation using the template-and-stack.yaml template

<img width="954" alt="5" src="https://github.com/user-attachments/assets/b477573c-1c73-4709-9891-5396ac6d5db9" />

3. The S3 bucket that was created using CloudFormation

<img width="953" alt="6" src="https://github.com/user-attachments/assets/6f4e7531-7513-4d0f-9c15-72f6f506dfa6" />

4. Modify the template to enable versioning on the S3 bucket to prevent objects from being deleted or overwritten

<img width="303" alt="7" src="https://github.com/user-attachments/assets/5db1e7da-51f1-449f-9951-4dbf2de41e4d" />

5. Update the stack on CloudFormation to use the modified template

<img width="956" alt="8" src="https://github.com/user-attachments/assets/defc0747-4bdd-438b-81ab-9ed309378ea9" />

6. Verify that versioning is enabled on the S3 bucket

<img width="696" alt="9" src="https://github.com/user-attachments/assets/2e333dee-f331-40d2-a1d7-45d1b379be1a" />

7. Clean up resources by deleting the stack


## Resources
The required Resources section in the CloudFormation template declares the AWS resources that you want to include in the stack

In the hands on lab, I will be doing the following: 
* Deploy an Ec2 instance via CloudFormation

1. Open the resources.yaml file and add the following to the template
* Format version
* Description
* Meta data
* Parameters
* Resources

<img width="350" alt="10" src="https://github.com/user-attachments/assets/4803002f-2fad-41fa-b31e-89f214603076" />

2. Create a stack on CloudFormation using the resources.yaml template

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

1. Open the intrinsic-functions.yaml template and add the following code to create a new parameter called **AmiID** 

<img width="241" alt="13" src="https://github.com/user-attachments/assets/af61cc0e-d021-40db-9573-db4019bad199" />

2. Use the intrinsic function **Ref** to pass the **AmiID** parameter input to the EC2 resource property

<img width="283" alt="14" src="https://github.com/user-attachments/assets/61681dae-4df8-4f02-a9f5-871535933c31" />

3. Add property **Tags** to the Properties section and reference **InstanceType** parameter, add *webserver*, delimited with a dash to the tags property

<img width="383" alt="15" src="https://github.com/user-attachments/assets/0be8fb6e-f1d4-4af0-a9cd-f60ad9c7f913" />

4. Create a stack on CloudFormation using the intrinsic-functions.yaml template. The tags that were successfully created.

<img width="495" alt="16" src="https://github.com/user-attachments/assets/db00855d-c5d9-4179-ba93-8580ed32f96a" />

5. Clean up resources by deleting the stack.


## Pseudo parameters
Pseudo parameters are parameters predefined by CloudFormation. You can use a pseudo parameter the same way you use a parameter.

In the hands on lab, I will be doing the following: 
* Leverage pseudo parameters for template portability best practices
* Identify sample use cases for leveraging pseudo parameters

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

6. Create a stack on CloudFormation using the pseudo-parameters.yaml template

<img width="956" alt="20" src="https://github.com/user-attachments/assets/1e3a5fc2-1933-4035-b2a4-091c5a4176b1" />

7. New resources are created and are shown in the Resources tab of the CloudFormation stack console

<img width="308" alt="21" src="https://github.com/user-attachments/assets/7d5da3df-e3b0-47ea-a67e-2d829be0302b" />

8. Verify the IAM permissions that were described in the template

<img width="707" alt="22" src="https://github.com/user-attachments/assets/1a9caf4a-62d3-4ccf-b267-a0d892cebbed" />

<img width="416" alt="23" src="https://github.com/user-attachments/assets/8705211b-2863-43ea-8424-3f3ff8354eaa" />

9. Verify that the Lambda function has the permissions to access the SSM parameter by manually invoking the Lambda function

<img width="953" alt="24" src="https://github.com/user-attachments/assets/3c7604d4-3596-410a-b7c9-96871d08715e" />

10. Clean up resources by deleting the stack

## Mappings
A mappings section is a top level section of a CloudFormation template. It is used to define maps, their keys and values which can be then referenced in the template. 

In the hands on lab, I will be doing the following:
* Create a mapping for environment type. Each environment type will be mapped to a different instance type.
* Find the required value in mappings and reference it in properties section of the EC2 resource

1. Open the mappings.yaml file, in the *Parameters* section replace the *InstanceType* with the following code.
 
<img width="412" alt="25" src="https://github.com/user-attachments/assets/f05d2bde-1677-434b-afe8-b148ab13ba98" />

2. Create *EnvironmentToInstanceType* in the mappings section

<img width="299" alt="27" src="https://github.com/user-attachments/assets/7dcd5cb2-5bbd-4907-b523-1f03fc39dcfc" />

3. Modify the *InstanceType* property

<img width="310" alt="28" src="https://github.com/user-attachments/assets/c8e23e43-d662-4a76-b46a-bef062650f2b" />

4. Update the Tags property

<img width="319" alt="29" src="https://github.com/user-attachments/assets/5b5d8f84-bbc1-48df-abaa-b1b0f96f1e63" />

5. Create a stack on CloudFormation using the mappings.yaml template

<img width="952" alt="30" src="https://github.com/user-attachments/assets/675a0c56-68c4-479a-b9b6-5cb79d0e96b4" />

6. Clean up resources by deleting the stack


## Outputs
Outputs enable you to get access to information about resources within a stack. Furthermore, output values can be imported into other stacks, these are known as cross-stack references. 

In the hands on lab, I will be doing the following:
* Create an Output section in the template and return the Public DNS name of the instance
* Learn how to view outputs from within CloudFormation in the AWS console

1. Open outputs.yaml file and add the following code to get the Public DNS name of the instance

<img width="341" alt="31" src="https://github.com/user-attachments/assets/f37d861c-0fa1-44db-aa25-f818defb6d0a" />

2. Create a stack on CloudFormation using the outputs.yaml template

<img width="950" alt="32" src="https://github.com/user-attachments/assets/0cccd487-9a20-4546-a8d5-1df20ea83080" />

3. View the output value in the Outputs tab of the CloudFormation console

<img width="438" alt="33" src="https://github.com/user-attachments/assets/1b491efa-8ef0-4381-ae50-bf544575cbb5" />

4. Clean up resources by deleting the stack


## Finding return values
Return values are documented in the AWS resource and property types reference for a given resource type, you can choose any resource type from the list and then choose **Return values** on the right side of the page to see which values you can use with intrinsic functions. 

In the hands on lab, I will be doing the following:
* Utilize return values of a resource in other resources described in the same template
* Define stack outputs based on the resource return values using intrinsic functions

1. Open the resource-return-values.yaml and add the following code

<img width="185" alt="34 1" src="https://github.com/user-attachments/assets/a32335fc-4d86-4f2a-afc4-934af42adcc3" />

2. Create a stack on CloudFormation using the resource-return-values.yaml template

<img width="956" alt="34" src="https://github.com/user-attachments/assets/53d868e4-152b-4f48-952d-2de48e813a31" />

3. View the resources that were created in the Resource tab of the CloudFormation console

<img width="439" alt="35" src="https://github.com/user-attachments/assets/335dd02d-046b-4f2d-ac3f-30c59158b83a" />

4. The bucket policy that was created

<img width="440" alt="36" src="https://github.com/user-attachments/assets/c8274ad3-6303-444d-820f-0ea95dfd5089" />

5. View the bucket domain name in the Outputs tab of the CloudFormation console

<img width="451" alt="37" src="https://github.com/user-attachments/assets/b6b6c4ef-5616-4a63-92c4-1a2ce37cf467" />

6. Clean up resources by deleting the stack


## Multi region latest AMI

In the hands on lab, I will be doing the following:
* Query AWS System Manager Parameter store in CloudFormation to get the latest Amazon Linux AMI ID
* Create a stack on CloudFormation in multiple regions

1. Open the multi-region-latest-ami.yaml file and update the AmiID parameter to the following

<img width="437" alt="1" src="https://github.com/user-attachments/assets/3f891e42-2a51-4158-af7d-3e5eacfe7cfb" />

2. Create a stack in the us-east-1 region using the multi-region-latest-ami.yaml template

<img width="947" alt="2" src="https://github.com/user-attachments/assets/a36f164f-7d81-4dea-ab8c-65e85c9e0b1c" />

3. Create a stack in the us-east-2 region using the multi-region-latest-ami.yaml template

<img width="955" alt="3" src="https://github.com/user-attachments/assets/1d2991b9-8240-4f6a-8386-1e4e9261466c" />

4. Clean up resources by deleting both of the stacks


## Session manager
Session manager is a fully managed AWS Systems Manager capability that lets you manage your Amazon EC2 instances through an interactive browser-based terminal or via the AWS CLI

In the hands on lab, I will be doing the following: 
* Create IAM role for the EC2 instance which grants access to the AWS Systems Manager
* Attach the IAM role o the EC2 instance
* Log in to the instance using SSM Session manager

1. Open the session-manager.yaml file and create an IAM role for the EC2 instance with the following code

<img width="455" alt="4" src="https://github.com/user-attachments/assets/f8844c79-8444-4159-a0a9-4d8a6a287877" />

2. Create an IAM instance profile using the following code

<img width="395" alt="5" src="https://github.com/user-attachments/assets/01127309-5cef-471f-8912-1466786cdd8d" />

3. Attach the IAM instance profile to the EC2 instance

<img width="528" alt="6" src="https://github.com/user-attachments/assets/c0d635bb-ad54-4172-b844-169a56f50275" />

4. Create the stack on CloudFormation using the session-manager.yaml template

<img width="946" alt="7" src="https://github.com/user-attachments/assets/25a02dbd-93ee-459e-9801-bf76cb110a6e" />

5. Connect to the EC2 instance using the SSM Session manager and retrieve the AMI ID from the instance metadata using the following command

<img width="395" alt="8" src="https://github.com/user-attachments/assets/58984f08-02ae-4ca5-b99b-acd0cfe267b8" />

6. Clean up resources by deleting the stack


## User data
User data scripts are executed as the **root** user, so there is no need to use sudo commands in the script. User data must be Base64 encoded when passed from CloudFormation to Ec2 instance. 

In the hands on lab, I will be doing the following:
* Bootstrap EC2 instance to install web server and content
* Create an EC2 security group and allow access on port 80 to the instance
* View the content served by the web server

1. Open the user-data.yaml and add the following code to create a security group

<img width="334" alt="9" src="https://github.com/user-attachments/assets/d9ee82e0-bde1-4992-9987-8c12feb15f65" />

2. Add an ingress rule in the security group to allow access from the Internet

<img width="512" alt="10" src="https://github.com/user-attachments/assets/51de23a2-7608-42e4-a96b-38f39a023c1f" />

3. Associate the security group withe EC2 instance

<img width="500" alt="11" src="https://github.com/user-attachments/assets/4815951e-812f-42ff-80e6-82251e2343e0" />

4. Install Apache web server on the instance using a User Data script

<img width="376" alt="12" src="https://github.com/user-attachments/assets/7fd4a42d-a706-4621-9546-e548f40e0c59" />

5. Add the WebsiteURL to the CloudFormation Outputs

<img width="506" alt="13" src="https://github.com/user-attachments/assets/3d9e2c67-9035-494a-946b-9782e2d99efb" />

6. Create the stack on CloudFormation using the user-data.yaml template

<img width="958" alt="14" src="https://github.com/user-attachments/assets/54057c2b-dbc1-4cd8-9717-c0c62972d735" />

7. View the outputs in the Outputs tab on the CloudFormation console and copy the website url

<img width="452" alt="15" src="https://github.com/user-attachments/assets/1f848c0b-87ad-4a2f-a7e7-5f912ebf3f3d" />

8. Paste the url in a new tab in the browser to see the web server that was created

<img width="947" alt="16" src="https://github.com/user-attachments/assets/316cae48-884b-4766-83d2-588c90dbefcd" />

9. Clean up resources by deleting the stack


## Helper Scripts
Helper scripts make CloudFormation a lot more powerful and enable you to fine tune templates to better fit your use case. 

In the hands on lab, I will be doing the following:
* Retrieve and interpret resource metadata, install packages, create files and start services with cfn-init
* Check for updates to metadata and execute custom hooks when changes are detected with cfn-hup
* Send a signal to CloudFormation when the resource or application is ready with cfn-signal

1. Open the helper-scripts.yaml file and add the following code to configure metadata

<img width="352" alt="17" src="https://github.com/user-attachments/assets/2492748e-8b46-4675-886d-20bbadd9d549" />

2.  Install the HTTD and PHP packages

<img width="433" alt="18" src="https://github.com/user-attachments/assets/c9ead49b-e14e-4fa7-98a2-488bc5316a04" />

3. Create index.php file

<img width="569" alt="19" src="https://github.com/user-attachments/assets/ad16711d-717a-4b3d-a04a-f64878fa6228" />

4. Enable and start the Apache web server

<img width="443" alt="20" src="https://github.com/user-attachments/assets/9d2de892-cb9f-474a-9063-a09ef266c584" />

5. Call the cfn-init script

<img width="515" alt="21" src="https://github.com/user-attachments/assets/c4118105-a958-4330-b97b-73ece490a33b" />

6. Configure cfn-hup

<img width="466" alt="22" src="https://github.com/user-attachments/assets/fb319a8f-e2d6-4409-8c25-8de1537fbf72" />

<img width="517" alt="23" src="https://github.com/user-attachments/assets/fe612b07-9cb5-4e31-ae33-903247bf6d45" />

<img width="347" alt="24" src="https://github.com/user-attachments/assets/ea2d3b98-0aad-429c-9fb0-ea899b67c27f" />

7. Configure cfn-signal and CreationPolicy attribute

<img width="506" alt="25" src="https://github.com/user-attachments/assets/ad1d9e63-d7a0-4954-9abe-c8f8088df936" />

8. Create a stack on CloudFormation using the helper-scripts.yaml template

<img width="952" alt="26" src="https://github.com/user-attachments/assets/2e9b4ec1-420f-4d32-9a26-35b7a21e8c6c" />

9. Verify that the instance was deployed, in a web browser enter the WebsiteURL which can be found in the Outputs tab of the CloudFormation console

<img width="953" alt="27" src="https://github.com/user-attachments/assets/1fbf464f-c0b9-4c85-8d88-8ea8508d154e" />

10. Clean up resources by deleting the stack


## Troubleshooting provisioning errors

In the hands on lab, I will be doing the following:
* Troubleshoot provisioning errors, whilst preserving the state of successfully deployed resources

1. Open the troubleshooting-provisioning-errors.yaml file

<img width="668" alt="28" src="https://github.com/user-attachments/assets/a37d1f61-9926-4ae1-86b6-01492e4f990c" />

2. Create a stack on CloudFormation using the troubleshooting-provisioning-errors.yaml template. In the **Stack failure options**, select **Preserve successfully provisioned resources**. The stack creation will fail because there is an error inside of the template.

<img width="956" alt="29" src="https://github.com/user-attachments/assets/95421779-6584-4a48-a72d-d09ff2cef9d3" />

3. In the **Resources** tab on the CloudFormation console, the DeadLetterQueue has been successfully created but the SourceQueue has failed create

<img width="429" alt="31" src="https://github.com/user-attachments/assets/7531d009-b246-4fa5-a0fb-275a9662aabc" />

4.  Open the troubleshooting-provisioning-errors.yaml file and fix the error

<img width="397" alt="30" src="https://github.com/user-attachments/assets/47802a13-244e-4771-b216-74ec600c75cf" />

5. Update the stack on CloudFormation using the updated template. The stack is now successfully created. 

<img width="954" alt="32" src="https://github.com/user-attachments/assets/3fe91ac2-667c-40a6-9fe6-89eda3025025" />

6. Clean up resources by deleting the stack
