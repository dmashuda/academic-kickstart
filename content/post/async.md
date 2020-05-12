+++
date = "2020-04-28T00:00:00"
draft = true
title = "An Intro To Message Queues"
summary = "What and Why?"
section_id = 0
+++


## Components of a Message Queue:

```mermaid
graph LR
    Start --> Message Queue --> Consumer
```

### 1.) The Queue

The queue is the application the recieves, holds, and distibutes messages

There are many options for message queues but here are some common ones:
 - [SQS](https://aws.amazon.com/sqs/)
 - [RabbitMQ](https://www.rabbitmq.com/)
 - [Azure Service Bus](https://azure.microsoft.com/en-us/services/service-bus/)


 ### 2.) The Messages
 The message is the data that is exchanged with the queue

 ### 3.) The Producer(s)
 The producer is the application that creates message and sends them to the queue

 ### 4.) The Consumer(s)
The producer is the application that receives messages from the queue, processes them, then marks the message as processed


## Why use a Message Queue?


### Decoupling

### Smoothing Workload Bursts 

### Batching Work

### Increasing reliability




Most interesting software(yes business software can be interesting) that we make and use interacts with external systems:
 - HTTP APIs
 - Email servers
 - File Systems
 - Databases

Each of these has a certian amount of flakiness(unreliability) and downtime as individuals. As we orchestrate multiple of these together the total unreliability of the combination of the services increases.


Let's take for example an HTTP endpoint in an imaginary web service for User signup for B2B product. What needs to be done?
 - Create some records in a database
 - Use an external subscription api to make a customer, create a subscription and give the user a free trial
 - Send the user a welcome email


 If we do all of theses things:
 ```
function createCompany(data){
  // Could fail if our database is down, but if our database is down that is pretty catastrophic
  insertCompany(data); 
  
  // Could fail if our email server is down, maybe the sysadmin wants to do some maintence in the middle of the day
  sendWelcomeEmail(data); 
  
  // External API's could fail
  createCustomerSubscription(data); 
}
 ```

In this situation we are depending on 3 different pieces of infrastructure, 2(email server/external api) are probably not the most reliable.
If any of the 3 calls fails, the user is going to get a nasty message.


Let's think about the same situation using queues:

 ```
function createCompany(data){
  // Could fail if our database is down, but if our database is down that is pretty catastrophic
  insertCompany(data); 
  
  // Could fail if the queue is unavailable
  emailQueue.send(data);

  // Could fail if the queue is unavailable
  createCustomerSubscriptionQueue.send(data);
  
}
 ```

 In this situation we are depending on 2 different pieces of infrastructure, 2(database/queue) are probably going to be more reliable.




 



