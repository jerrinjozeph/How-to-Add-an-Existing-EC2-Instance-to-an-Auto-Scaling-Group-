# How to Add an Existing EC2 Instance to an Auto Scaling Group
In a typical AWS environment, Auto Scaling Groups (ASGs) automatically launch new instances based on a predefined launch configuration or template. However, there are specific scenarios where you might need to bring a pre-existing EC2 instance under the management of an ASG.
This post provides a simple, professional guide on how to achieve this, ensuring your specific instance benefits from the ASG’s monitoring and replacement capabilities.

--------------------------------------------------------------------------------
## Step 1: Prepare Your Instance and Create an AMI
Before making any changes, you must ensure the existing instance is healthy.
- Reboot and Verify: Reboot the instance and confirm that all applications or sites are loading correctly.
- Create an AMI: Once verified, create an Amazon Machine Image (AMI) of the instance. This AMI serves as a blueprint (containing snapshots of the attached disks) that the ASG will use if it needs to recreate the instance later.
## Step 2: Configure a Launch Template
To manage the instance, the ASG requires a Launch Template. Use the following details based on the original instance:
- AMI: Select the AMI you just created.
- Instance Type: For example, t2.micro.
- Networking: Ensure the Key Pair and Security Group match the requirements of your existing setup.
## Step 3: Set Up the Auto Scaling Group
When creating the ASG, the goal is to initialize it without immediately launching new, unwanted instances.
- Network Settings: Use the same VPC and Subnets where the existing instance resides.
- Group Size: Set the Desired capacity to 0 and Minimum capacity to 0. Set the Maximum capacity to 1.
- Note: By starting with a desired capacity of 0, the ASG will stay empty until you manually attach your instance.
## Step 4: Attach the Instance
Once the ASG is ready, you can officially move the existing instance into the group:
1. Navigate to the EC2 Instances list in your AWS Console.
2. Select your specific instance.
3. Go to Actions > Instance Settings > Attach to Auto Scaling Group.
## The Result: Automated Monitoring
Once attached, the ASG begins continuous monitoring of the instance status. If the instance fails or stops for any reason, the ASG will automatically trigger the creation of a replacement instance using the Launch Template you configured, ensuring your application stays online
