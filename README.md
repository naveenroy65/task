# task
# Java Application CI/CD with Jenkins

This project demonstrates a **CI/CD pipeline for a Java application** using Jenkins and Maven.  
The pipeline is defined in the `Jenkinsfile` and automates the process of **checkout, build, test, and deploy**.

---

## Pipeline Overview

The Jenkins pipeline (`Jenkinsfile`) contains the following stages:

1. Checkout from SCM  
   - Pulls source code from GitHub (`main` branch).  
   - Uses the configured Jenkins credentials (`github`) for authentication.  

2. Build  
   - Runs `mvn clean compile` to compile the Java project.  

3. Test
   - Executes unit tests with `mvn test`.  

4. Deploy  
   - Packages the application using `mvn package`.  
   - Confirms successful packaging with a deployment message.  

---

 Prerequisites

Before running the pipeline, ensure the following:

- Jenkins installed and running (either on a server, VM, or container).  
- Maven 3 is installed and configured inside Jenkins (`Global Tool Configuration`).  
- Java JDK 11 (or higher) installed and configured in Jenkins if required.  
- Jenkins has the following plugins installed:  
  - Pipeline 
  - Git  
  - Maven Integration 

---

## Jenkins Setup

1. Clone this repository into your Jenkins workspace:  
   ```bash
   git clone https://github.com/naveenroy65/task
2.Run the Build Pipeline.
