# Hosting an application on Cloud-Architecture

Created a visual diagram on how i would host an application on the AWS cloud, based on the knowledge i acquired as a AWS cloud Practitioner Certificate Holder.

1. Static Content (Frontend App):
      - Used Amazon S3 for hosting static assets (HTML, CSS, JavaScript).
      - linked S3 to S3 Glacier in an Another availability Zone in the VPC in case of failure of the original Amazon S3.
      - Distributed my content via Amazon CloudFront, a CDN for global delivery with low latency.

2. Virtual Private Cloud (VPC)
      - Created a VPC to isolate my application infrastructure:
      - Use private subnets for database and backend services.
      - Use public subnets for EC2 instances that need direct internet access (if necessary).
      - Split my VPC in 2 Availability Zones for fault tolerance and redundancy.

3. Created 1 Public and 2 Private Subnets
      - Public Subnet:
          Used an internet Gateway to allow access to the public subnet coupled with auto scaling and security groups for added security.
          This will allow users to access records that they might need about their accounts.
      - Private Subnet 1:
          All of the S3 object will be sent to this subnet and AWS Lambda will delete all the data we deem unnecessary and backup the rest in Amazon S3 Glacier in another availability           Zone in case the first S3 fails.
      - Private Subnet 2:
          This subnet coupled with a securtiy group will store all of the data needed to run the application and there will also be a backup of the data running in another availabilty           zone.

4. Security Groups
      - Added security groups to all of the Subnets for security Puroses.

5. High Availability and Fault Tolerance
      - Every service that I utelized has a backup in another Availabilty zone in case of failover. (Ex: EC2, Amazon S3, Aurora).

6. Scalability
      - Enabled auto scaling for the EC2 instances.

7. Monitering and Alerts
      - Used Amazon Cloud watch to monitor matrics, logs and set up alarms. also used Amazon SNS attached to the VPC in case a failure happens so we can be notified.


ACTUAL DIAGRAM

          
