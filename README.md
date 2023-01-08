# udacity-devops-project-02

### Deploy a high-availability web app using CloudFormation
This project shows hands-on experience on infrastructure as code (IaC). A realistic scenario where a dummy application is deployed (a sample JavaScript or HTML file) to the Apache Web Server running on an EC2 instance.

<br>

There is two parts to this project:

- Diagram: You'll first develop a diagram that you can present as part of your portfolio and as a visual aid to understand the CloudFormation script.

*Below is the diagram that shows the infrastructure this project builds*
<div style= "background: black;">
<p align="center">
  <img src="/diagram/Udacity_project_2.png"
       alt="Udacity_project_2"
  >
</p>
</div>


- Script (Template and Parameters): The second part is to interpret the instructions and create a matching CloudFormation script.

##### Starter Code
A starter code was for the project in this [Github repository](https://github.com/udacity/nd9991-c2-Infrastructure-as-Code-v1). 

<br>

## Getting Started 
#### Scenario

Your company is creating an Instagram clone called Udagram.

Developers want to deploy a new application to the AWS infrastructure.

You have been tasked with provisioning the required infrastructure and deploying a dummy application, along with the necessary supporting software.

This needs to be automated so that the infrastructure can be discarded as soon as the testing team finishes their tests and gathers their results.

Optional - To add more challenge to the project, once the project is completed, you can try deploying sample website files located in a public S3 Bucket to the Apache Web Server running on an EC2 instance. Though, it is not the part of the project rubric.


#### Server specs

You'll need to create a Launch Configuration for your application servers in order to deploy four servers, two located in each of your private subnets. The launch configuration will be used by an auto-scaling group.
You'll need two vCPUs and at least 4GB of RAM. The Operating System to be used is Ubuntu 18. So, choose an Instance size and Machine Image (AMI) that best fits this spec.
Be sure to allocate at least 10GB of disk space so that you don't run into issues. 
Security Groups and Roles


Since you will be downloading the application archive from an S3 Bucket, you'll need to create an IAM Role that allows your instances to use the S3 Service.
Udagram communicates on the default `HTTP Port: 80`, so your servers will need this inbound port open since you will use it with the Load Balancer and the Load Balancer Health Check. As for outbound, the servers will need unrestricted internet access to be able to download and update their software.
The load balancer should allow all public traffic `(0.0.0.0/0)` on `port 80` inbound, which is the default HTTP port. Outbound, it will only be using port 80 to reach the internal servers.
The application needs to be deployed into private subnets with a Load Balancer located in a public subnet.
One of the output exports of the CloudFormation script should be the public URL of the LoadBalancer. Bonus points if you add `http://` in front of the load balancer DNS Name in the output, for convenience.


### Other Considerations


1. You can deploy your servers with an SSH Key into Public subnets while you are creating the script. This helps with troubleshooting. Once done, move them to your private subnets and remove the SSH Key from your Launch Configuration.

2. It also helps to test directly, without the load balancer. Once you are confident that your server is behaving correctly, increase the instance count and add the load balancer to your script.

3. While your instances are in public subnets, you'll also need the SSH port open (port 22) for your access, in case you need to troubleshoot your instances.

4. Log information for UserData scripts is located in this file: `cloud-init-output.log` under the folder: `/var/log`.

5. You should be able to destroy the entire infrastructure and build it back up without any manual steps required, other than running the CloudFormation script.

6. The provided UserData script should help you install all the required dependencies. Bear in mind that this process takes several minutes to complete. Also, the application takes a few seconds to load. This information is crucial for the settings of your load balancer health check.

7. It's up to you to decide which values should be parameters and which you will hard-code in your script.

8. See the provided supporting code for help and more clues.

9. If you want to go the extra mile, set up a bastion host (jump box) to allow you to SSH into your private subnet servers. This bastion host would be on a Public Subnet with `port 22` open only to your home IP address, and it would need to have the private key that you use to access the other servers.



<br>

## Dependencies
##### 1. AWS account
You would require to have an AWS account to be able to build cloud infrastructure.

##### 2. VS code editor
An editor would be helpful to visualize the image as well as code. Download the VS Code editor [here](https://code.visualstudio.com/download).

### How to run the supporting material?
You can run the supporting material in two easy steps:
```bash
# Ensure that the AWS CLI is configured before runniing the command below
# Create the network infrastructure
# Check the region in the create.sh file
./create.sh myFirstStack network.yml network-parameters.json
# Create servers
# Change the AMI ID and key-pair name in the servers.yml
# Check the region in the update.sh file
./update.sh mySecStack servers.yml server-parameters.json
```

<br>


## How to run it
The infrastructure can be created with the command below :

```
./create.sh [stackName1] network.yml network-parameters.json
./create.sh [stackName2] servers.yml servers-parameters.json
```

<br>

## Contact
Kingsley Ocran - [https://github.com/kingsleyocran/](https://github.com/kingsleyocran/)