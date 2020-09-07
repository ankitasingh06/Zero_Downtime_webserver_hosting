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
5.1 If launching first time then create a deployment of the pod using the image created in the previous job. Else if deployment already exists then do rollout of the existing pod making zero downtime for the user.
5.2 If Application created first time, then Expose the application. Else don’t expose it.

# Tools and Technology used :-
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
Image for post
» Static node:- Static node includes making Jenkins slave to a different VM which will work when Master will assign job to them.
Otherwise they will sit idle .
» Dynamic node:-this is to resolve the limitation of static nodes i.e. Reducing the power usage of static node when they are idle, reducing provisioning cost , Reducing storage problem etc.
Dynamic launching of node can be done by the use of containerization technology.

![1_49JemATeH1NHlD04jr9Kqw](https://user-images.githubusercontent.com/60088271/92413893-be9f5b80-f16f-11ea-9874-7617266b44f6.png)



