# AWS-Step-Function
In this article you will get to know how to create a Dynamo DB table in AWS cloud using Step Function.

What is AWS Step Function?
AWS Step Functions is a serverless function orchestrator that makes it easy to sequence AWS Lambda functions and multiple AWS services into business-critical applications. Through its visual interface, you can create and run a series of checkpointed and event-driven workflows that maintain the application state.

To create a Step Function:
1. Log into your AWS Console and search for AWS step function in the search menu.
2. Press get started to create your first step function.
3. Here choose create your own workflow from scratch.


    ![image](https://github.com/AnuV541/AWS-Step-Function/assets/110184106/edbc4e36-d0cb-40f7-b20b-a43359cf2873)


4. This is the workflow studio of aws step function.
   

   ![image](https://github.com/AnuV541/AWS-Step-Function/assets/110184106/94ac06c7-a316-44f4-a1ac-a802c95411d5)


6. From actions search for dynamoDB and choose the create function.
7. Drag and drop the function to the machine graph.


   ![image](https://github.com/AnuV541/AWS-Step-Function/assets/110184106/4bf19be2-6937-445f-a10e-558f3ad34a26)


8. Leave all the configuration of the table as default. Now to to code section and change the json code to as follows.


 ```
   {
  "Comment": "A description of my state machine",
  "StartAt": "CreateTable",
  "States": {
    "CreateTable": {
      "Type": "Task",
      "End": true,
      "Parameters": {
        "AttributeDefinitions": [
          {
            "AttributeName": "movie",
            "AttributeType": "S"
          }
        ],
        "KeySchema": [
          {
            "AttributeName": "movie",
            "KeyType": "HASH"
          }
        ],
        "TableName": "MyData1",
        "ProvisionedThroughput": {
          "ReadCapacityUnits": 5,
          "WriteCapacityUnits": 5
        }
      },
      "Resource": "arn:aws:states:::aws-sdk:dynamodb:createTable"
    }
  }
}
```


9. Now go to config section and give a name for youe state machine and select assign a new role.


    ![screencapture-us-east-1-console-aws-amazon-states-home-2023-10-12-23_34_44](https://github.com/AnuV541/AWS-Step-Function/assets/110184106/7f0dee62-2b17-4b1b-bf05-16975906c311)


10. After that you will be directed to the following. Press confirm.
   
   
    ![image](https://github.com/AnuV541/AWS-Step-Function/assets/110184106/07ab4126-8a83-463a-a204-97d7b1ee38ff)



11. After this go to IAM and select the role which was just created or go to the IAM roles page by selecting the role arn. Here add another policy which gives the user full access to dynamo db.


    ![screencapture-us-east-1-console-aws-amazon-iamv2-home-2023-10-12-23_41_24](https://github.com/AnuV541/AWS-Step-Function/assets/110184106/728781a2-68fb-4950-9845-1e0c35b9411e)


12. After this go to the work flow and start the execution. In few minutes you can see a dynamo db table created with the specified configuration.


    ![image](https://github.com/AnuV541/AWS-Step-Function/assets/110184106/c73c9a32-c8b0-48cb-a38b-6bbd448d3414)

    
    ![image](https://github.com/AnuV541/AWS-Step-Function/assets/110184106/a61b3af9-e017-4082-9e02-b03cf0a6adaa)


    ![image](https://github.com/AnuV541/AWS-Step-Function/assets/110184106/f5fb1ebd-c7a2-4067-97ff-66a2d7e5cb79)

