# Udacity's Cloud DevOps Engineer Project 2

## Deploy a High-Availability Web App Using CloudFormation

In this project, you’ll find the cloudformaation code to deploy web servers for a highly available web app using CloudFormation that i coded as part of this project. Using these files you can create and deploy the infrastructure and application for an Instagram-like app from the ground up. You will begin with deploying the networking components followed by servers, security roles and software and do it exactly as it’s done on the job: following best practices and scripting as much as possible.


## Requirenments

### Server specs:
- create a Launch Configuration for your application servers in order to deploy four servers, two located in each of your private subnets. The launch configuration will be used by an auto-scaling group.

- You'll need an Ubuntu 18 System with 2 vCPUs, 4GB of RAM, 10GB of disk space.

### Security Groups and Roles:

- Creat an `IAM Role` that allows your instances to use the `S3` Service. 

- Udagram communicates on the default `HTTP Port: 80`; your servers will need this inbound port open since you will use it with the Load Balancer and the Load Balancer Health Check.

- The load balancer should allow all *inbound* traffic `(0.0.0.0/0)` on `port 80`, which is the default *HTTP port*. Also, it will only be using `port 80` *(outbound)* to reach the internal servers.

- The application will be deployed into private subnets with a Load Balancer located in a public subnet.

- One of the output exports of the CloudFormation script will be the public URL of the LoadBalancer.(Bonus points for adding `http://` in front of the load balancer *DNS Name*).




### Other Considerations:

- The SSH port (`port 22`) in the servers are open, in case you need to troubleshoot your instances. Note: You need to add `keyname` to the server *Launch Configuration* cloudformation code.

- There is file that sets up a bastion host to allow you to SSH into your private subnet servers. This bastion host will be on a Public Subnet with `port 22` open only to your *home IP address*, and it would need to have the private key that you use to access the other servers.

- Log information for UserData scripts is located in this file: `cloud-init-output.log` under the folder: `/var/log`.

- You will be able to destroy the entire infrastructure and build it back up without any manual steps required, other than running the CloudFormation scripts.

- The *UserData script* used for the servers *Launch Configuration* was provided by Udacity to help install all the required dependencies. Bear in mind that this process takes several minutes to complete. Also, the application takes a few seconds to load. This information was crucial for the settings of the load balancer health check.