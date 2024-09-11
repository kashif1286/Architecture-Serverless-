
# Architecture Serveless

Start a Architecture Serveless project using AWS services

# creat a project

I am uses 4 service(IAM role, Lambda, Dynamodb, S3, application for runing project)

# Lab overview and high desing
lest's start 

![Blank diagram - Page 1](https://github.com/user-attachments/assets/dc0d6701-b5fb-4f9e-bb0d-c8c704641751)

The overview of serverless architecture project 

# 1. Create a IAM role

![iam 1 1](https://github.com/user-attachments/assets/8b5da9b6-85a2-4505-93ce-f7a054f625c1)

![iam 1 2](https://github.com/user-attachments/assets/acb7b2c4-23a4-4f3c-9c52-513fff3264da)

![iam 1 3](https://github.com/user-attachments/assets/42e0d390-0640-4c1f-b7e8-ffb64400a84c)

![iam 1 4](https://github.com/user-attachments/assets/e9cd9ec1-3eb8-4fdd-a514-c1af2fccf24f)

![iam 1 5](https://github.com/user-attachments/assets/c0432bf9-3852-4ebc-bcf9-1a35e17c3aad)

![iam 1 6](https://github.com/user-attachments/assets/b4115936-f0a5-45f2-9115-11506d8ac47a)

![iam 1 7](https://github.com/user-attachments/assets/c6909181-94ef-459c-b025-188d4077fd78)

# 2. Create DyanamoDB

![db 2 1](https://github.com/user-attachments/assets/714dce82-3a9d-4a76-8f47-ae9670b12067)

![db 2 2](https://github.com/user-attachments/assets/78e4ac42-c085-4e95-8390-845ad052cd41)

![db 2 3](https://github.com/user-attachments/assets/173b155f-f50e-4f0c-b733-7bc34724a1f8)

# 3. Create S3 Bucket

![s3 3 1](https://github.com/user-attachments/assets/9715d34e-02b2-4acc-9521-8f454dcb8456)

![s3 3 2](https://github.com/user-attachments/assets/eecf3830-395c-4acd-a513-d99d9267dae8)

![s3 3 3](https://github.com/user-attachments/assets/f0370962-2fcd-4ffd-902f-a5f3ad64077b)

# 4. Creat a Lambda Fuction

![L 4 1](https://github.com/user-attachments/assets/2e8e45e2-0216-4751-b6a3-77e0449b9125)

![L 4 2](https://github.com/user-attachments/assets/352261be-317f-449c-b30a-104b32d175cc)

![L 4 3](https://github.com/user-attachments/assets/bf9d8c01-ab7f-4c3c-a7a6-af8b78ff5a3d)

```bash

import json
import boto3

s3_client = boto3.client('s3')
dynamodb = boto3.resource("dynamodb")
table = dynamodb.Table('grras_lambda')

def lambda_handler(event, context):
    try:
            
        bucket_name = event["Records"][0]["s3"]["bucket"]["name"]
        s3_file_name = event["Records"][0]["s3"]["object"]["key"]
        
        response = s3_client.get_object(Bucket=bucket_name, Key=s3_file_name)
        data = response["Body"].read().decode('utf-8')
        employees = data.split("\n")
        for emp in employees:
            try:
                emp = emp.split(",")
                table.put_item(
                    Item = {
                        "id": str(emp[0]),
                        "Name": str(emp[1]),
                        "City": str(emp[2]),
                        "passcode": str(emp[3]),
                        "contry": str(emp[4])
                    }
                   )
            except:
                continue
    except Exception as err:
        print (err)
        
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }

```
add the s3 bucket name (copy) and paste (table = dynamodb.Table('grras_lambda'))  in this line means = (grras_lambda ) remove the name and pest S3 bucket name


![L 4 4](https://github.com/user-attachments/assets/fa55c702-7a24-4a8c-b3e6-b2aac5621241)

![L 4 5](https://github.com/user-attachments/assets/3ace0621-e6fc-4d70-a6a4-22d55e344468)

add exel file in S3 bucket and copy file name and paste line no .30 
and in line no.23 paste bucket name

and click the save button

![L 4 6](https://github.com/user-attachments/assets/fa71e54b-70b5-4b1d-8028-636d421dfc7b)

![L 4 7](https://github.com/user-attachments/assets/0247e317-d8d7-40c6-a83e-b1b72853558a)

cheak the Dynamo Db items table and 

![RUN project](https://github.com/user-attachments/assets/3c919979-4715-46bc-97bc-d2ba2812d179)

congratulation your project is runing

# delete all services

THank you comming my repository and guit hub account and cheak my project











