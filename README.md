# jenkins-cmake-experimentation
[Link towards the jenkins server (read access for everyone without authentication)](http://34.1.13.140/)
[![Build Status](http://34.1.13.140/buildStatus/icon?job=jenkins-cmake-experimentation&build=18)](http://34.1.13.140/job/jenkins-cmake-experimentation/18/) 
A training c++ project, built and tested by jenkins and cmake  
The project has a MathFunctions library to compute the square root of a number.   
There is a webhook which triggers the Jenkins pipeline at every push.  
The Jenkinsfile build and test all the project on a docker image I created on the Jenkins server.  
The tests results are generated in a JUnit xml file, and they are visible directly on the Jenkins console.  

