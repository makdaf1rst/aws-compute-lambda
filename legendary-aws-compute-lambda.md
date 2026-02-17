<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Fetch Data with AWS Lambda

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-lambda)

**Author:** saqibh49@gmail.com  
**Email:** saqibh49@gmail.com

---

## Fetch Data with AWS Lambda

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-compute-lambda_p9thryj2)

---

## Introducing Today's Project!

In this project, I will demonstrate how to pull data from a DynamoDB table using a Lambda function. I'm doing this project to learn how serverless functions work in a web app so I'm better prepared for future projects working on production environments. 

### Tools and concepts

Services I used were Lambda, DynamoDB and IAM. Key concepts I learnt include Lambda functions, IAM permission policies, and Lambda function testing. 

### Project reflection

This project took me approximately 1 hour. The most challenging part finding some of the items on the Lambda function page, like the policy permissins, which wasn't super obvious that I needed to click the user's name to get to. It was most rewarding to see the data from my table start populating during my Lambda function's test run. 

I chose to do this project today because I'm very interested in cloud engineering and want to know everything I need to know to have a rewarding career in the field someday. Something that would make learning with NextWork even better is if there was a text editor area in the lesson where I could practice my javascript and json syntax. 

---

## Project Setup

To set up my project, I created a database using a partition key.  The partition key is userID, which means my data will be sorted by each user's ID

In my DynamoDB table, I added an item with some sample user data. DynamoDB is schemaless, which means I don't have to define all my columns upfront like I would with a relational database — I can just add whatever attributes I need to each item, and different items can even have different attributes.

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-compute-lambda_a112c3d5)

### AWS Lambda

AWS Lambda is a service that runs code without needing to manage any computers/servers. Lambda manages them for the user. I'm using Lambda in this project to connect to and retrieve data from my DynamoDB table. 

---

## AWS Lambda Function

My Lambda function has an execution role, which is a basic IAM role that gives the Lambda function access to only what it needs and nothing more. By default, the role grants access to write logs to CloudWatch. 

My Lambda function will take userID as an input and search for data related to it in my DynamoDB table. 

The code uses AWS SDK, which is a library of prewritten code that makes it easier for developers to connect to AWS services for their apps. My code uses SDK to communicate with DynamoDB. 

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-compute-lambda_a1b2c3d5)

---

## Function Testing

To test whether my Lambda function works, I used a command that asks Lambda to search for data related to the userId 1. The test is written in JSON. If the test is successful, I'd see the user information I uploaded to my table related to the userId of 1. 

The test displayed a 'success' because the code ran successfully, indicating no issues in the code, but the function's response was actually denied because we haven't given our Lambda function permission to access DynamoDB yet. 

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-compute-lambda_u1v2w3x4)

---

## Function Permissions

To resolve the AccessDenied error I'm adding a DynamoDB read-only policy to it so it can retrieve data from DynamoDB but not be able to edit it. 

There were four DynamoDB permission policies I could choose from, but I didn't pick ExecutionRole nor Invocation roles because they only allow for streaming changes to the table, like a news feed and makes Lambda take immediate action on data, respectively. Neither lets me just retrieve the data. 

I also didn't pick FullAccess because that gives my function read, write, delete and update access, which is more than it needs. If my function ever became exposed, that would also make the rest of my data insecure as well.  AmazonDynamoDBReadOnlyAccess was the right choice because it provides GET access without allowing editing or deleting capabilities. 

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-compute-lambda_3ethryj2)

---

## Final Testing and Reflection

To validate my new permission settings, I reran my test command. The results were successful because with the ReadOnlyAccess policy attached to my function, it was able to retrieve the relevant data from my table. 

Web apps are a popular use case of using Lambda and DynamoDB. For example, I could have Lambda search a DynamoDB table when a user tries to login.  

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-compute-lambda_p9thryj2)

---

## Enahancing Security

For my project extension, I challenged myself to use an inline policy. This will give me more granular control over my function's permissions. In this case, I will use an inline policy to allow my function to only access the UserId table instead of all DynamoDB tables. 

To create the permission policy, I used he console because I've used JSON multiple times already so I think it's good idea to get an idea of te other method of doing things. 

When updating a Lambda function's permission policies, you could risk breaking its access to other AWS services if you remove or change the wrong permissions. I validated that my Lambda function still works by running a test that asks it to retrieve data associated with a certain attribute.

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-compute-lambda_1qthryj2)

---

---
