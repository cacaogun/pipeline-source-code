# pipeline-source-code
My CI/CD pipeline to deploy app to AWS Fargate

Explore the application and review the Fargate configuration

![image](https://github.com/cacaogun/pipeline-source-codes/assets/103553102/0f2d1fc2-7a3e-4087-a558-30fa6a805cf8)

However, to launch this application on Amazon ECS and build a pipeline that automates its deployment, you need three additional files:

•	buildspec.yaml: CodeBuild uses the commands and parameters in the buildspec file to build a Docker image.

•	appspec.yaml: CodeDeploy uses the appspec file to select a task definition.

•	taskdef.json Recall that all three tasks that are currently running in your Amazon ECS service reference the same task definition. After updating the application source code and building a new container, you need a second task definition that points to it. The taskdef.json file is used to create this new task definition that points to your updated application image.


I built a blue/green deployment that uses this modified application code in the green environment.
 To change the application background color to green, enter the following command:
 
 ``
 sed -i 's/282F3D/1D8102/g' ~/environment/static/css/app.css
 ``
 
 I prepare blue/green deployment by creating a CodeDeploy application and deployment. An application is a name that uniquely identifies the code that you want to deploy. 
 
 CodeDeploy uses deployment groups to specify the Amazon ECS service, load balancer, and target groups for your revised application code. They also include configuration details, such as how and when traffic should be rerouted to the new tasks that your pipeline creates.
 

 ![image](https://github.com/cacaogun/pipeline-source-codes/assets/103553102/d0bcbdf0-5ba5-401e-b32b-4bcafadd294f)
 

Finally, I use CodePipeline to configure a pipeline that automates the release process for your application. When complete, the pipeline invokes whenever CodeCommit detects changes. At this point, CodeBuild builds a new image, pushes it to Amazon ECR, and then CodeDeploy deploys the new image to your Amazon ECS cluster.

![image](https://github.com/cacaogun/pipeline-source-codes/assets/103553102/4e0c6482-b50f-4670-9858-c7a9cb633d32)


All stage succeeded~ And the application background changes to green~
