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
## Jenkins Setup

1. place this repository into your Jenkins workspace:  
   ```bash
    https://github.com/naveenroy65/task.git

<img width="1848" height="844" alt="image" src="https://github.com/user-attachments/assets/25fe4163-1444-47f3-ab4f-2d1ad43f3a27" />
<br>
<br>
<br>

 Prerequisites

Before running the pipeline, ensure the following:

- Jenkins installed and running (either on a server, VM, or container).  
- Maven 3 is installed and configured inside Jenkins (`Global Tool Configuration`).  
- Java JDK 11 (or higher) installed and configured in Jenkins if required.  
- Jenkins has the following plugins installed:  
  - Pipeline 
  - Git  
  - Maven Integration 
  <br>
  <br>
<img width="1780" height="616" alt="Screenshot 2025-09-24 191830" src="https://github.com/user-attachments/assets/c9ca3b64-5e9f-497c-be16-a89a216aa133" />
<br>
<br>
<br>
<img width="1616" height="689" alt="Screenshot 2025-09-24 191844" src="https://github.com/user-attachments/assets/9b75d36f-b12a-4c58-aaea-af621d368793" />
<br>
<br>

---

2.Run the Build Pipeline.
<br>
<br>
<img width="1617" height="233" alt="image" src="https://github.com/user-attachments/assets/14e5d5a2-e172-4bbb-83b7-292c2fdc536f" />
<br>
<br>
<br>
<img width="1901" height="747" alt="image" src="https://github.com/user-attachments/assets/9bf4bdb0-0bc1-4e67-9638-2db8bdacbbaf" />

