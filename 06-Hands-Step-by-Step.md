# Step 1: Setting up Instance/VM

First, we need to create a ubuntu server on cloud solutions like AWS, Azure etc. or in virtual machine. In my case I’ve created my ubuntu server on VM.

![Image](https://github.com/user-attachments/assets/95706e9f-1c33-4773-9f79-740d777941a9)

Now we have to ssh to the server using ssh <server_name>@<ip_address> or cloud ssh -i pem_file_location <server_name>@<ip_address>

# Step 2: Installing & Setting up Jenkins on Server

**1. Update packages**

```
sudo apt update
```

**2. Install JDK (Jenkins requires it)**

```
sudo apt install openjdk-17-jre -y
```

**3. Add Jenkins key, repo and install**

```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
Then we have to access the Jenkins using ip address and port. Default installation port is 8080.
Ex: 10.132.173.223:8080

![Image](https://github.com/user-attachments/assets/3d3b13d2-e5b3-4265-af34-e7d56ded5b8a)

We have to find the admin password by running the command shown in the screenshot.

![Screenshot 2025-04-17 150658](https://github.com/user-attachments/assets/9dc84b50-bc73-4088-af9b-20c1a0a608a5)

Click on the Install Suggested Plugins

Then we have to configure the Jenkinsfile using SCM method.

![Image](https://github.com/user-attachments/assets/dffabb3a-5500-46e0-8ea0-7a21f589ce97)

![Image](https://github.com/user-attachments/assets/fbd87906-868d-4df1-b983-315e3f4205aa)

Since we've used Docker Agent method. The whole jenkins pipeline will run on docker container. The custom image which I've created it will be pulled automatically and the best part is maven is also included in the image. My dockerhub profile link: [https://hub.docker.com/repositories/waserkarim]. So, we don't have to create extra steps for maven setup. When the pipeline will end the docker container will be removed and this allow us to optimize our pipeline. Which is very cost effective and good solution. 

##Installing Plugins

**Docker:**

![Image](https://github.com/user-attachments/assets/22d02931-4069-4d16-9b04-a059049a319a)

**Sonarqube:**

![Image](https://github.com/user-attachments/assets/45089c08-9ab1-4bf2-af0f-6ebe4fa750a2)

# Step 3: Sonarqube Server Install

**Configure a Sonar Server locally**

System Requirements
Java 17+ (Oracle JDK, OpenJDK, or AdoptOpenJDK)
Hardware Recommendations:
   Minimum 2 GB RAM
   2 CPU cores

```
sudo apt update && sudo apt install unzip -y
adduser sonarqube
sudo su - sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.4.1.88267.zip
unzip *
chown -R sonarqube:sonarqube /opt/sonarqube
chmod -R 775 /opt/sonarqube
cd /opt/sonarqube/bin/linux-x86-64
./sonar.sh start

```
By default SonarQube runs on 9000 port
Now you can access the `SonarQube Server` on `http://<ip-address>:9000`

![Image](https://github.com/user-attachments/assets/945b81dc-d8d4-4c74-a662-1ea078cb36fd)

![Image](https://github.com/user-attachments/assets/ebe3a9b6-02f1-47ee-8add-62751445929a)

After accessing the Sonarqube the default user credentials will be username and pass will be: admin

![Image](https://github.com/user-attachments/assets/4e7a2bbe-fe48-4625-bbe7-8472de33e1b3)

Jenkins and Sonarqube is two diffrent applications. So, need to create a token for Jenkins so that Jenkins can access the Sonarqube.

![image](https://github.com/user-attachments/assets/0ccfdc23-7df6-4965-8b0a-c480e5da62d6)

![Image](https://github.com/user-attachments/assets/f9e274bb-a37d-41c6-959f-9e1ffeab32d6)

Now in Jenkins we have to go to: Dashboard > Manage Jenkins > Credentials > System > Global credentials (unrestricted)
Then we have to set the screat text.

![Image](https://github.com/user-attachments/assets/2d3e2112-3b0e-412e-a13b-0a4ef3f77367)

Step 4: Installing Docker on Instance/VM

**Docker Slave Configuration**

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```

**Grant Jenkins user and Ubuntu user permission to docker deamon.**

```
sudo su -
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```

Once you are done with the above steps, it is better to restart Jenkins.

```
http://<ec2-instance-public-ip>:8080/restart
```

The docker agent configuration is now successful.

![Image](https://github.com/user-attachments/assets/e1e95d1d-06bc-43d7-9690-9795c6074688)

![Image](https://github.com/user-attachments/assets/73c034ff-15d2-4311-ac43-6f7ca85545fe)

Once you are done with the above steps, it is better to restart Jenkins.

```
http://<ec2-instance-public-ip>:8080/restart
```

![Image](https://github.com/user-attachments/assets/6c0095d9-d1de-42c5-8a86-e9229106472b)

# Step 5: Kubernetes and ArgoCD setup on local device

## 1. If the [Chocolatey Package Manager](https://chocolatey.org/) is installed, use the following command:

```
choco install minikube
```

## **2. Start your cluster**

From a terminal with administrator access (but not logged in as root), run:

```
minikube start
```

Copy

If minikube fails to start, see the [drivers page](https://minikube.sigs.k8s.io/docs/drivers/) for help setting up a compatible container or virtual-machine manager.

## **3. Interact with your cluster**

If you already have kubectl installed (see [documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl/)), you can now use it to access your shiny new cluster:

```bash
kubectl get po -A
```
![Image](https://github.com/user-attachments/assets/66831cb3-e0ef-475f-baf1-48fc05d8583b)

## 2. Download Argo CD CLI[](https://argo-cd.readthedocs.io/en/stable/getting_started/#2-download-argo-cd-cli)

Download the latest Argo CD version from https://github.com/argoproj/argo-cd/releases/latest. More detailed installation instructions can be found via the [CLI installation documentation](https://argo-cd.readthedocs.io/en/stable/cli_installation/).

Also available in Mac, Linux and WSL Homebrew:

```bash
brew install argocd
```

## 3. Access The Argo CD API Server[](https://argo-cd.readthedocs.io/en/stable/getting_started/#3-access-the-argo-cd-api-server)

By default, the Argo CD API server is not exposed with an external IP. To access the API server, choose one of the following techniques to expose the Argo CD API server:

### Service Type Load Balancer[¶](https://argo-cd.readthedocs.io/en/stable/getting_started/#service-type-load-balancer)

Change the argocd-server service type to `LoadBalancer`:

```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

### Ingress[](https://argo-cd.readthedocs.io/en/stable/getting_started/#ingress)

Follow the [ingress documentation](https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/) on how to configure Argo CD with ingress.

### Port Forwarding[¶](https://argo-cd.readthedocs.io/en/stable/getting_started/#port-forwarding)

Kubectl port-forwarding can also be used to connect to the API server without exposing the service.

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

The API server can then be accessed using https://localhost:8080


