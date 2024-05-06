
# ROS1 CI Project Setup

## Prerequisites

0. **Verify Git Authenticity:**  
   Ensure that the connection to the repository is secure. Execute the command below in the ROSject terminal to confirm:
   ```bash
   git ls-remote -h -- git@github.com:vallab/ros1_ci.git HEAD
   ```
   user:~$ git ls-remote -h -- git@github.com:vallab/ros1_ci.git HEAD
   The authenticity of host 'github.com (4.208.26.197)' can't be established.
   ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
   Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
   Warning: Permanently added 'github.com,4.208.26.197' (ECDSA) to the list of known hosts.

1. **Setting Up Jenkins:**  
   If Jenkins isn't already running (check using `pf faux | grep jenkins`), follow these instructions to get it up and running. A shell script to install the latest version of Jenkins is available within the ROSject. Run these commands in your ROSject terminal:
   ```bash
   source ~/.bashrc
   cd ~/webpage_ws/ && bash start_jenkins.sh
   ```

2. **Accessing Jenkins:**  
   You can open the Jenkins dashboard using one of two methods:
   - **Via Proxy Address:**  
     Run this command to retrieve the proxy URL, then click the link to open Jenkins:
     ```bash
     jenkins_address
     ```
   - **From Text File:**  
     Use this command to read the file that holds the Jenkins URL:
     ```bash
     cat ~/jenkins__pid__url.txt
     ```

## Jenkins Credentials

1. **Login to Jenkins:**  
   Use the credentials below to sign in to the Jenkins web interface:
   ```text
   Username: admin  
   Password: password  
   ```

## Using Jenkins

1. **Managing the "ros1_ci" Project:**  
   On the Jenkins dashboard, locate the "ros1_ci" project. You can manually initiate a build by pressing the "Build Now" button on the project page. Alternatively, commit changes to the repository to automatically trigger a build.

2. **Building via Pull Request:**  
   - Add a new `test.txt` file to the repository and open a pull request.
   - Once merged, navigate to the "ros1_ci" project page or the Build Executor tab in Jenkins.
   - Wait briefly (less than a minute) for the build to start automatically due to the SCM change.
   - Click the build dropdown to view the "Console Output" and observe the build process.
   - The build will pull a Docker image and proceed with building and testing.
   - After successful completion, check the ROSject tab for these outcomes:
     - Gazebo will launch with the TortoiseBot Playground world.
     - The Waypoint action server will start.
     - TortoiseBot will navigate to the predefined waypoint.
   - Once the waypoint is reached, Gazebo will close.
   - Review the Jenkins Console Output for a summary of the ROS test, which should pass.

## Important Note
Occasionally, Gazebo may not start promptly, causing the test to fail. If this happens, manually rebuild the project in Jenkins.
