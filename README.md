# Adding an existing instance to an AutoScalingGroup
Recently i've encountered a case where the client enquired whether we can add an exisitng instance to an Auto Scaling Group.
Usually Instances are added to the asg group based on the launch configuration/launch template details but client specifically need to add a particular instance to the ASG.
# Created an AMI of the instance to be added
Before creating an AMI of an instance make sure to reboot the instance and check whether the sites are loading fine after reboot.
AMI Name : shopping-app
while creating an AMI usually a snapshot of a disk involved is taken , we can create a volume from snapshot and an instance from an AMI, AMI is nothing but snapshots of the disk attached the instance.
# Creating a launch template for ASG
name: shopping-app-lc
AMI: which we've created from the instance client mentioned.
instance type: t2.micro
key pair: mumbai
SecurityGroup: Freedom
# Creating ASG
Name: shopping-asg
lc: shopping-app-lc
VPC: same vpc as the instance
Subnets: In these subnets the instances will be created.
Load balancer is not attached with ASG and no health check configured.
Desired: 0 Min: 0 & Max:1 ( so here only 1 instance can be accomadated, and intially no instance will be created coz of desired 0).
No scaling policies involved
Tagging the instance created as same name as client's instance.
# Attaching the clients instance to ASG
Instance > Actions > Attach to ASG
# Now ASG created with the clients instance 
![image](https://github.com/user-attachments/assets/1f240d47-2ef7-43a7-8bdd-7175520f85f9)
# If we stop the running instance
As the instance is attached to the ASG there will be continous monitoring on the instance status and if the status got down , new instance will be created with launch template.
