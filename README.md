# Zero_Downtime_webserver_hosting

![1_PzlKUWgDXjjiHssaS7VE2A](https://user-images.githubusercontent.com/60088271/92413832-81d36480-f16f-11ea-870a-dd0d3a78ec86.jpeg)

This is a project based on hosting website at ZERO DOWNTIME!! Zero Downtime describes a site without service interruption. To achieve such lofty goals, redundancy becomes a critical requirement at every level of your infrastructure.

As all leading business depends on their regular,continuous and easy service providence , trust of their users/customers with various Business strategies. for ex.- Amazon , flipkart , Netflix, youtube etc.

This all depends on the Deployment Architecture. None of the users want any type of delay in their work just for downtime. Obviously they will move/switch to the another Website.

So here the role of Automation come into play , as none of the business guys intentionally wants their service to go down.As for them this business is their bread and butter , they are earning money because of their services.So with the help of Automation we can resolve this issue of downtime.

Here is one of my Project which depends on to deploy our Web server using a very good feature of Jenkins that is Distributed Jenkins.

# Project Task:-
1. Create container image that’s has Linux and other basic configuration required to run Slave for Jenkins. ( example here we require kubectl to be configured )
2. When we launch the job it should automatically starts job on slave based on the label provided for dynamic approach.
3. Create a job chain of job1 & job2 using build pipeline plugin in Jenkins
4. Job1 : Pull the Github repo automatically when some developers push repo to Github and perform the following operations as:
4.1 Create the new image dynamically for the application and copy the application code into that corresponding docker image
4.2 Push that image to the docker hub (Public repository)
( Github code contain the application code and Dockerfile to create a new image )
5. Job2 ( Should be run on the dynamic slave of Jenkins configured with Kubernetes kubectl command): Launch the application on the top of Kubernetes cluster performing following operations:
- 5.1 If launching first time then create a deployment of the pod using the image created in the previous job. Else if deployment already exists then do rollout of the existing pod making zero downtime for the user.
- 5.2 If Application created first time, then Expose the application. Else don’t expose it.

# Tools and Technology used :-
- RedHat Virtual Machine
- git
- github
- jenkins
- docker
- kubernetes

# Theory :-
Master Slave Architecture :- A Jenkins master comes with the basic installation of Jenkins, and in this configuration, the master handles all the tasks for your build system. The job of a Slave is to do as they are told to, which involves executing build jobs dispatched by the Master.

![1_JfXwsBSoRu1Q0CsEnqxfuQ](https://user-images.githubusercontent.com/60088271/92413867-a7606e00-f16f-11ea-90c6-473912c8109d.png)

As we that there can be two types of Slave nodes in Jenkins(Master Slave Architecture)
- 1.Static node
- 2.Distributed/Dynamic node

![1_49JemATeH1NHlD04jr9Kqw](https://user-images.githubusercontent.com/60088271/92413893-be9f5b80-f16f-11ea-9874-7617266b44f6.png)

» Static node:- Static node includes making Jenkins slave to a different VM which will work when Master will assign job to them.
Otherwise they will sit idle .

» Dynamic node:-this is to resolve the limitation of static nodes i.e. Reducing the power usage of static node when they are idle, reducing provisioning cost , Reducing storage problem etc.
Dynamic launching of node can be done by the use of containerization technology.



# Procedure :-
•Step 1:- Creation of docker image with the help of Dockerfile.
   - For dynamic launching of kubernetes, we are creating docker image for kubernetes

![1_9DYjmkQ5QE1Vb2v0S000QQ](https://user-images.githubusercontent.com/60088271/92445492-0e167380-f1d2-11ea-84ee-9c1d82de5086.jpeg)

I created ssh_config file , which I have created for the ssh authentication.

![1_cHlCvp8C1dQHzCr7HaTt4g](https://user-images.githubusercontent.com/60088271/92445711-5c2b7700-f1d2-11ea-848a-8af29df04177.png)

2. For Launching Web server:-

![1_DkHRfbqHJP8JXkj0KbPKQg](https://user-images.githubusercontent.com/60088271/92445806-85e49e00-f1d2-11ea-861f-0cd7b9bb6e8c.jpeg)

Now with the help of docker docker push <container_name>
I just checked this image , whether it is working fine or not, by launching it first time.
docker push ankita0610/webserver-html:v2
code inside index.html in ankita0610/webserver-html:v2 :-
""<html>
<body bgcolor=”aqua”>
<h1>Hello World!!</h1>
<h3>My first webpage</h3>
</body>
</html>""

![1_xQUMoajriELWjar0Qk8YYg](https://user-images.githubusercontent.com/60088271/92445859-9a289b00-f1d2-11ea-932e-6e5a8ec91bb2.jpeg)

Now we gonna change our website with zero downtime.This is what our practical is.
Step 2:- Creation of Dynamic node(Dynamic cloud)
-Go to manage jenkins
-Go to Manage node and clouds
-Go to configure cloud
-And do following steps

![1_i-uWJF3MYkDXzKlFrwn0Wg](https://user-images.githubusercontent.com/60088271/92445921-b0365b80-f1d2-11ea-96f7-2ad25e379cda.jpeg)

![1_Is1wALe7vxkoYNqTxg0JWA](https://user-images.githubusercontent.com/60088271/92445998-cfcd8400-f1d2-11ea-922a-4ac55d98fd18.jpeg)

![1_mDXpFv_UDtptYmk3FxVdew](https://user-images.githubusercontent.com/60088271/92446034-de1ba000-f1d2-11ea-863c-2a3727620864.jpeg)

![1_sXFCdXc0ooVQfdyWQxuScg](https://user-images.githubusercontent.com/60088271/92446085-ee337f80-f1d2-11ea-9ffa-bfdefe8c05ba.jpeg)

Now , we have to create web-hook on github so that as soon as developer push their program file on github, github will trigger our job1.

![1_1eJXADAabpBBnfr1HHlpLA](https://user-images.githubusercontent.com/60088271/92446271-33f04800-f1d3-11ea-8bdd-f7d780ba7331.jpeg)

![1_o-msNlHGtF4WYUKn5UQG6g](https://user-images.githubusercontent.com/60088271/92446322-49657200-f1d3-11ea-8fc2-b4a900da933d.jpeg)

Now to create jobs in jenkins:-
Job 1:- job1 will pull the repository from github and copy the files/content from workspace to our local directory.
- Create the new image dynamically for the application and copy the application code into that corresponding docker image
- Push that image to the docker hub (Public repository)
( Github code contain the application code and Dockerfile to create a new image )

![1_DD4smt2SDLNGEmODUMlayg](https://user-images.githubusercontent.com/60088271/92446609-afea9000-f1d3-11ea-93c1-877994002ef0.jpeg)

![1_F-sTvcYSbuA8KfX9Ih1geQ](https://user-images.githubusercontent.com/60088271/92446652-c09b0600-f1d3-11ea-8fec-baa4fb06500d.jpeg)

And here is the output on Build of job1.

![1_QJFSeH8CRdCnAw9PPVsjbQ](https://user-images.githubusercontent.com/60088271/92446702-d6a8c680-f1d3-11ea-964d-b4f9eb020d43.jpeg)

![1_ODXEmbaQGnRn5smjrc8WFQ](https://user-images.githubusercontent.com/60088271/92989311-ffd99780-f4f0-11ea-84dd-1a744dd08b3e.jpeg)

![1_uxlnFkwum6iXLf33UcbLFQ](https://user-images.githubusercontent.com/60088271/92989322-141d9480-f4f1-11ea-845b-e1c09749fa7f.jpeg)

Job2:- For launching the slave node dynamically and then deploy the webserver.
- If launching first time then create a deployment of the pod using the image created in the previous job. Else if deployment already exists then do rollout of the existing pod making zero downtime for the user.
- If Application created first time, then Expose the application. Else don’t expose it.
Code of index.html in ankita0610/webserver-html:v3 :-
""<html>
<body bgcolor=”orange”>
<h1>Hello World!!</h1>
<h3>My first webpage</h3>
</body>
</html>""

![1_yvS3ptJNPKqssW1r8HLK0w](https://user-images.githubusercontent.com/60088271/92989332-34e5ea00-f4f1-11ea-93a8-a464220e0d48.jpeg)

![1_q4dDZHaHG3PeFdNLH9PYsw](https://user-images.githubusercontent.com/60088271/92989338-45966000-f4f1-11ea-87c4-f8138332d622.jpeg)

I have created deploy.yml program file for creating deployment, and it will use the container image, which I have pushed into docker hub in job1.

![1_s1zd38CZcv0NRiklwSqYpQ](https://user-images.githubusercontent.com/60088271/92989346-5f37a780-f4f1-11ea-83e7-c62414ea9f9e.png)


![1_5GRMl1PNWv33xuZIK3QXZQ](https://user-images.githubusercontent.com/60088271/92989358-74143b00-f4f1-11ea-9caf-a933dac974ea.jpeg)

And here is the output of Build of Job2


![1_ZVTwdswOfGIkKdvv0EPc6A](https://user-images.githubusercontent.com/60088271/92989367-87bfa180-f4f1-11ea-9859-7598d0356b44.png)

![1_41UF1riPUNRBJRSBt79XRQ](https://user-images.githubusercontent.com/60088271/92989378-9b6b0800-f4f1-11ea-98b9-b7df344eb490.jpeg)

![1_WS_iopnS54nuPSgkueW9ZQ](https://user-images.githubusercontent.com/60088271/92989389-b0479b80-f4f1-11ea-94db-5cebdc0f8606.jpeg)


Here is build pipeline view:-

![1_yqHdLggio4Mjcj978RAXaA](https://user-images.githubusercontent.com/60088271/92989401-c190a800-f4f1-11ea-93a2-75f76bfe6c11.jpeg)

Here is the output , which I get:-

![1_TQo4SJDdQI1vN2Sh8gdkNQ](https://user-images.githubusercontent.com/60088271/92989417-d66d3b80-f4f1-11ea-9d96-9a8d8a28fcaa.jpeg)

So this is how we launched our website with no downtime, ZERO DOWNTIME!! with the use of DevOps automation tools .

