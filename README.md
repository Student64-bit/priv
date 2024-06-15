## Overview

This project demonstrates creating a Continuous Integration and Continuous Deployment (CI/CD) pipeline using Jenkins, SonarQube, and Docker. Engineers can commit code to GitHub, which will then be checked and analyzed by SonarQube for errors. If the code passes the analysis, it will be deployed by Docker. Jenkins is used to automate this process, where a GitHub webhook triggers Jenkins to start the pipeline.

## Services Used

- **AWS EC2**: Created three instances—one for Jenkins, one for SonarQube, and another for Docker.
- **Jenkins**: Used for continuous integration when changes are committed to GitHub.
- **SonarQube**: Analyzes code for issues/bugs automatically when code is committed to the pipeline via GitHub.
- **Docker**: Deploys the application automatically once tests pass from SonarQube.
- **GitHub**: Stores my resume website HTML file and Dockerfile and triggers Jenkins with a webhook upon code commits.
- **HTML**: Displays my resume webpage.

## Steps

### Step 1: Creating the Basic Setup

For this step, I started by creating a basic HTML webpage to be displayed. Then, I set up three separate EC2 instances: one for Jenkins to handle continuous integration, another for SonarQube to check and analyze the code, and the last one for Docker deployment.

<p align="center">
  <img src="Images/jen1.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: The three EC2 instances that will be used in my CI/CD pipeline.</small>
</p> 
<br>

### Step 2: Setting Up Jenkins

Next, I shelled into my Jenkins instance and installed a Java JRE. This allowed me to install Jenkins on the instance. After installing Jenkins, I went into my EC2 instance's security group and opened port 8080 so that I could configure Jenkins settings via the internet using my instance's IP. I then used the `systemctl status jenkins` command to get my secret key, which I needed to set up Jenkins properly. Inside the Jenkins configuration, I provided my GitHub link along with the correct branch and selected ‘GitHub hook trigger for GITScm polling’ to enable continuous integration whenever changes are made to GitHub.

<p align="center">
  <img src="Images/jen2.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Exposing port 8080 so that I can use the Jenkins dashboard when it’s set up in my EC2 instance.</small>
</p>
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen3.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Jenkins is up and running on the instance. Although I will clean up after this project and the IP address will no longer be in use, it's generally a good practice to avoid exposing or displaying IP addresses. This caution helps protect against potential bad actors, even if the instance is virtual.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen4.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Installing default plugins via the Jenkins dashboard.</small>
</p> 
<br>


### Step 3: Testing the Jenkins Pipeline

To test the Jenkins pipeline I previously created, I set up a webhook for my GitHub repository. To check if everything was working, I created a new text file in my GitHub repository called ‘Jenkins Test’. Once I committed and pushed the file, I checked Jenkins to see if it triggered the pipeline, which it did. This confirmed that the pipeline up to this point was functioning automatically.

<p align="center">
  <img src="Images/jen5.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Setting up my webhook to invoke Jenkins whenever code is committed to my GitHub repository.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen7.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Initial Jenkins build, so that I can test continuous integration.</small>
</p>
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen9.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Console output</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen8.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Pipeline before the test commit to GitHub.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen10.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Test file that I’m going to commit to my GitHub repository to test that Jenkins is continuously integrating changes I have committed (Filename 'Jenkins test').</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen11.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Build after the commit.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen12.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Success, Jenkins integrated the commit from Jenkins into the pipeline which is proof of continuous integration.</small>
</p> 
<br>


### Step 4: Setting Up SonarQube

For this step, I configured and set up SonarQube on my second EC2 instance for continuous code analysis. This involved installing all the necessary components, including SonarQube, and exposing port 9000 so I could use the web GUI with the instance IP. From there, I set up and generated a token to use in Jenkins. After the configuration, I built my pipeline and checked on the SonarQube website to see if my code passed the test, which it did. This meant I could now deploy the passed code to Docker, tying up my project where I can commit code, and if it passes, it will be continuously deployed to Docker.

<p align="center">
  <img src="Images/jen13.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Used 'wget' command to install SonarQube on my instance and used the unzip command to retrieve its contents.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen14.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: SonarQube is up and running.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen15.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Generating a SonarQube token so that SonarQube can be implemented into my Jenkins pipeline.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen16.png" alt="error" width="80%" height="80%">
  <img src="Images/jen17.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Installing appropriate Jenkins plugins to use with SonarQube.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen18.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Configuring the SonarQube scanner on Jenkins.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen19.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Configuring the SonarQube server on Jenkins.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen21.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Configuring the SonarQube token.</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen25.png" alt="error" width="80%" height="80%">
  <br>
  <small>Project Image: Finally, after configuring SonarQube to work with Jenkins, I rebuilt my pipeline and SonarQube is successfully scanning and checking for code errors continuously/automatically whenever a commit is made to my GitHub repository.</small>
</p> 
<br>

### Step 5: Configuring Docker

In my third and final instance, the task was to set up Docker so that Jenkins on my first instance could connect to the Docker server to implement continuous deployment for my simple HTML resume website when I commit changes to GitHub. To test that things were working, I ran remote executable commands from Jenkins. I did ‘touch test.txt’ from Jenkins to make sure when I built and updated my pipeline, the test.txt file would appear inside my Docker instance, which it did. Then, I created a Dockerfile on GitHub and ran commands to ensure that when I committed changes to GitHub, they were reflected on the Docker instance. As shown below, my resume website has been deployed and set up for continuous integration, analysis (with SonarQube), and deployment with Docker.

<p align="center">
  <img src="Images/jen26.png" alt="error" width="80%" height="80%">
  <br>
<small>Project Image: Installing & setting up docker on my instance</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen28.png" alt="error" width="80%" height="80%">
  <br>
<small>Project Image: Configuring docker jenkins implementation, exposing it to port 22</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen29.png" alt="error" width="80%" height="80%">
  <br>
<small>Project Image: Configuring my docker server implementation on jenkins </small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen30.png" alt="error" width="80%" height="80%">
  <br>
<small>Project Image: Now that docker is setup into my jenkins pipeline, im going to test for continious deployment by running a simple shell command to create a file in my docker instance </small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen31.png" alt="error" width="80%" height="80%">
  <br>
<small>Project Image: Success, the test file was created into my docker file from the jenkins pipeline via a remote shell command</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen32.png" alt="error" width="80%" height="80%">
  <br>
<small>Project Image: Now im going to test for contiously deployment with the orignal application itself which is my html resume</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen33.png" alt="error" width="80%" height="80%">
  <img src="Images/jen34.png" alt="error" width="80%" height="80%">
  <img src="Images/jen35.png" alt="error" width="80%" height="80%">
  <img src="Images/jen36.png" alt="error" width="80%" height="80%">
  <br>
<small>Project Image: With the help of nginx and scp commands remotetly from the jenkins pipeline I was able to contiously/automatically deploy my website application within my pipeline with docker</small>
</p> 
<br>
<br>
<br>

<p align="center">
  <img src="Images/jen37.png" alt="error" width="80%" height="80%">
  <br>
<small>Project Image: My application has now been deployed in my CI/CD pipeline.</small>
</p> 
<br>

## Issues Encountered

- **Jenkins Performance**: The Jenkins dashboard was incredibly slow, so I upgraded the AWS EC2 instance to a larger size with higher compute power.

<p align="center">
  <img src="Images/jen24.png" alt="error" width="80%" height="80%">
  <br>
<small>Project Image: Upgrading my instances from t2.micro to t2.medium for more memeory and computing power</small>
</p> 
<br>
<br>
<br>

- **SonarQube Integration**: The Java community JDK used was outdated. Console logs from Jenkins helped identify this issue, which was resolved by creating a new Java 17 JDK run path file.

<p align="center">
  <img src="Images/jen22.png" alt="error" width="80%" height="80%">
  <img src="Images/jen23.png" alt="error" width="80%" height="80%">
  <br>
<small>Project Image: Implementing the new java 17 sdk path for jenkins, since the older updated path was giving me errors.</small>
</p> 
<br>
<br>
<br>
  
- **Lost Jenkins Password**: Lost the Jenkins user password stored in a text file. Resolved by editing the XML file in the Jenkins instance, setting `<security>false</security>`, accessing the dashboard without login credentials, and resetting the password. Improved future password management practices to avoid such issues.

- - **Amazon web services direct shell connect issue**: I ran into an issue when trying to connect jenkins to my docker service via the aws browser shell. I believe the issue had to do with authentication, which I decicded to manually login to my shell via my local command line using the .pem key provided when I was setting up my instances.
 
<p align="center">
  <img src="Images/jen27.png" alt="error" width="80%" height="80%">
  <br>
  <strong><small>Project Image: Upgrading my instances from t2.micro to t2.medium for more memeory and computing power</small></strong>
</p> 
