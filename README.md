# devopsproject-liftAndshift
This is an IAAS project to host a website using AWS Cloud. VMs are launched to host different services i.e. RabbitMQ, Memcache, Maria DB &amp; Tomcat 9. AWS is used as the cloud provider for the Infrastructure.

The code artifacts are uploaded to the S3 using AWS CLI. A new IAM role is created with S3 access which is then attached to the Application VMs so that the artifacts in S3 can be downloaded and set up in the application VM.

First three VMs are launched in AWS to host the following services:
1. RabbitMQ ->Used for Messaging Que
2. Memcache -> To cache
3. Maria DB -> Used for Database operations

Above services were launched in separately and set up in the CentOS9 VMs

A new Ubuntu VM is launched and Tomcat service is installed in the VM. The application is hosted in this VM.
Separate Security Groups were launched for the Load Balancers, Application VM and for Backend services i.e. RabbitMQ, Memcache & Maria DB.
Inbound Rules are configured from ELB to Application VM, and Application VM to Backend services groups.

A new Target group is created with the instances. A new ELB is launched with the Target Group configured.
In the DNS, a new CNAME record is created with ELB DNS endpoint configured.

For Autoscaling, a new launch configuration is created and an Autoscaling group is set up as per the load.

Source Code can be downloaded from: https://github.com/hkhcoder/vprofile-project/tree/main/src
