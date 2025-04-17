# Installation

## For Linux Setup

### 1. Update packages

```bash
sudo apt update
```

### 2. Install JDK (Jenkins requires it)

```bash
sudo apt install openjdk-17-jre -y
```

### 3. Add Jenkins key, repo and install

```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

### 3. Check Jenkins status

```bash
sudo systemctl status jenkins
```

## For Windows Setup

**Pre-requisite:** Oracle JDK needs to be installed.  

JDK Download Link for Windows10/11:

[Download the Latest Java LTS Free](https://www.oracle.com/java/technologies/downloads/)

**Setting up environment variables:**

We have to copy the path of the JDK which we just installed. It is located in: C:\Program Files\Java\jdk<JDK VERSION WHICH WE INSTALLED>\bin

![Image](https://github.com/user-attachments/assets/6c968794-db64-43b2-8135-051a2d09f292)

After setting environment variables just download and install the Jenkins on windows. 

Jenkins Download Link for Windows10/11: 

[Thank you for downloading Windows Stable installer](https://www.jenkins.io/download/thank-you-downloading-windows-installer-stable/)

Then we have to access the Jenkins on localhost by hitting it on the browser. Ex. locahost:8090. After that basic setup screens will be there. We just need to go through them.

![Image](https://github.com/user-attachments/assets/78823aff-78e7-42ee-98bc-655e915de157)

After going through the whole process. The initial homepage looks like this.
