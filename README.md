# AWS Elastic Beanstalk Deployment Guide

Follow these steps to deploy your application on AWS Elastic Beanstalk with an RDS database.

## Prerequisites

1. **Create an AWS Account**: Ensure you have an AWS account with a valid credit card.

2. **Create a Budget**: Set up a budget and select the "Zero free tier" option.

3. **Create IAM Role**: Create an IAM role named `aws-ec2-service-role` with the policy `AmazonEC2ContainerServiceRole`.

## Elastic Beanstalk Environment Setup

1. **Create EB Environment**:
   - Select `aws-ec2-service-role` for EC2 instance profile.
   - Create RDS with the instance type `db.t3.micro`.
   - Set up environment variables.

2. **Update Front End Project**:
   - Change `REACT_APP_SERVER_URL` to the EB domain URL.
   - Replace all instances of localhost.
   - Rebuild the front-end project.

3. **Database Connection**:
   - Try to connect using pgAdmin.

4. **VPC Security Group Inbound Rule**:
   - Create a rule allowing all traffic.

5. **Update Production Host**:
   - Change the production host to `DB_HOSTNAME`.

6. **Update .env File**:
   - Add the following to your `.env` file:
     ```
     DB_DATABASE=rest-rant
     DB_USERNAME={your username}
     DB_PASSWORD={your password}
     DB_HOSTNAME={your RDS endpoint}
     ```

7. **Database Migration**:
   - Run the command: `npx sequelize-cli db:migrate`.

8. **RDS Parameter Group**:
   - Create a parameter group with `rds.force_ssl` set to 0.
   - Assign the parameter group to RDS.

9. **Reboot Database**.

10. **Seed Data**:
    - Run the command: `npx sequelize-cli db:seed`.

11. **Update EB Environment Variables**:
    - Add the following to your EB environment variables:
      ```
      DB_DATABASE=rest-rant
      DB_USERNAME={your username}
      DB_PASSWORD={your password}
      DB_HOSTNAME={your RDS endpoint}
      ```
