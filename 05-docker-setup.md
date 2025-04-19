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
