**Explain how you setup CI/CD in your current organization**

**Version:1** \
I have used Jenkins for the CICD, and I'll be using Git for source code management, and I'll be maintaining my source code over there.
So we have different types of source code like Golang, Java based, ReactJS based code. 
So I'll be cloning the source code using git clone and by mentioning the URL, branch name and credentials ID. 
So we have stored these credentials in the Jenkins credential sections, and we'll be generating the credentials ID. I'll be using that in my pipeline. 

So the first stage will be cloning the source code, and then building the source code using Maven or NPM tools based on my application type.
If it is a Java based application, I will be using Maven, and if it is Reactjs and Node Js applications, I will be using npm tools. 
And if it is a Golang or Python, I don't need any build stage.
Directly I can add the source code to the Docker file, and then I will be pushing these changes to the SonarQube for the quality checks, 
like we have a quality gate and quality policies are there. I'll be using them for checking my code quality and then executing the automated test cases like Selenium. 

So once the build process is done, I'll be adding the source code to the Docker file and creating an image out of it, 
and using that image, I'll be pushing it to the Docker registries like Jfrog, Nexus or ECR Artifactory Docker registries, 
and I'll be adding this image into the Kubernetes manifest files, and I'll be deploying it on the Kubernetes. 

So afterwards, we'll be having post Build actions. Are there things like success or failure?

**Version:2**
We'll be deploying these with help of Helm charts to the Kubernetes environments. 
And we'll be having a post build actions or post deployment actions, whether it is a successful or failure
