<---> Implemented CI/CD project using AWS <---> 

In this project, you have utilized AWS CodeBuild, CodePipeline, and CodeDeploy to create a CI/CD pipeline for deploying an application onto an EC2 instance. AWS SSM Parameter Store was used to securely store Docker credentials. 
The project involved the following steps

--->  Integrating AWS SSM Parameter Store
Store Docker credentials in AWS SSM Parameter Store as secure strings.


--->Setting Up AWS CodeBuild
Create a new build project in the CodeBuild console.
Configure the source, environment, and buildspec file. The buildspec.yml file defines the build commands and settings.
Save the project and note the ARN for later use in the CodePipeline.


--->Creating the EC2 Instance and Installing Docker and CodeDeploy Agent:
aunch an EC2 instance from the AWS Management Console.
Select an appropriate AMI.
Choose an instance type (e.g., t2.micro for small applications).
Configure the security group to allow necessary ports (e.g., 22 for SSH, 80/443 for HTTP/HTTPS).

* Install docker
	--> sudo apt update
	--> sudo apt install docker.io
* Install CodeDeployAgent
	--> sudo apt update
	--> sudo apt install ruby-full
	--> sudo apt install wget
	--> wget https://bucket-name.s3.region-identifier.amazonaws.com/latest/install
	--> chmod +x ./install
	--> sudo ./install auto
	--> systemctl status codedeploy-agent
	--> systemctl start codedeploy-agent
	--> systemctl restart codedeploy-agent

--->Creating an IAM Role for CodeDeploy
Create another role for CodeDeploy.
Select the type of trusted entity as "AWS service" and choose "CodeDeploy".
Attach the AWSCodeDeployRole policy.
Name the role and create it.


--->Creating an IAM Role for EC2 Instance:
Go to the IAM console and create a new role.
Select the type of trusted entity as "AWS service" and choose "EC2".
Attach the AmazonEC2RoleforAWSCodeDeploy policy.
Name the role and create it.


--->Creating a CodePipeline
Go to the CodePipeline console and create a new pipeline.
Choose a source provider (e.g., GitHub) and connect your repository.
Set up a build provider (AWS CodeBuild).
Add a deploy provider (AWS CodeDeploy).
Review and create the pipeline.


--->Deploying with CodeDeploy
In the CodeDeploy console, create a new application.
Create a new deployment group and attach the IAM role created for EC2.
Specify the deployment settings and EC2 instances.
Define the AppSpec file (appspec.yml) to specify the deployment actions.
