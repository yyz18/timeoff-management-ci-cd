# Timeoff-management application CI/CD

<br>
<br>
<p align="center">
Architecture Diagram
<br>
<br>
<img src="https://user-images.githubusercontent.com/36462985/222253330-7151db25-6585-4262-9b1f-e9f2849e5229.png" width="700">
</p>

The imeoff-management application is accessible at [https://venisso.com](https://venisso.com). Any attempt to access it using http address is automatically redirected to https, thereby ensuring secure communication between the client and the application server.
</p>


<h3> Technology Stack </h3>
<p>
The pipeline is implemented in AWS utilizing some open sources tools. The following is a list of the tools employed:
</p>

__GitHub__ serves as the source code management repository 

__Jenkins__ implements CI/CD pipeline 

__Ansible__ packages the application into a docker image and uploads it to Docker Hub 

__Docker Hub__ stores the application docker image 

__Kubernetes__ runs application containers 

__eksctl__ is used to create the Kubernetes cluster 

__kubectl__ is used to manage the Kubernetes cluster 
   __AWS__ Certificate Manager issues public certificate for SSL/TLS encryption

<h3> Workflow </h3>
<p>
  Whenever there are changes in the code, it is pushed to the GitHub repository, which triggers a Jenkins CI job. This job then copies the complete application onto the Ansible server and runs an Ansible playbook to containerize it into a Docker image. It then uploads the image to a Docker Hub repository. Once the CI job is completed successfully, the CD job starts.

  The CD job runs Kubernetes manifest scripts to create a deployment and a service on the Kubernetes cluster, which consists of three nodes distributed across three different availability zones. The deployment is designed to facilitate rolling updates while ensuring at least one healthy node is maintained at all times, resulting in zero downtime.
  
  The network connection between a client's browser and the application server is made secure through the provision of SSL/TLS certificates by AWS.
</p>

