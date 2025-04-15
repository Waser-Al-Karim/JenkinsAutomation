# Installation

## Linux Setup

### 1. Update packages

```bash
sudo apt update
```

### 2. Install JDK (Jenkins requires it)

```bash
sudo apt install openjdk-17-jdk -y
```

### 3. Add Jenkins key and repo

```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
```

### 4. Install Jenkins

```bash
sudo apt install jenkins -y
```

### 5. Start and enable Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

### 6. Check Jenkins status

```bash
sudo systemctl status jenkins
```

## Windows Setup

**Pre-requisite:** Oracle JDK needs to be installed.  

JDK Download Link for Windows10/11:

[Download the Latest Java LTS Free](https://www.oracle.com/java/technologies/downloads/)

**Setting up environment variables:**

We have to copy the path of the JDK which we just installed. It is located in: C:\Program Files\Java\jdk<JDK VERSION WHICH WE INSTALLED>\bin



After setting environment variables just download and install the Jenkins on windows. 

Jenkins Download Link for Windows10/11: 

[Thank you for downloading Windows Stable installer](https://www.jenkins.io/download/thank-you-downloading-windows-installer-stable/)

Then we have to access the Jenkins on localhost by hitting it on the browser. Ex. locahost:8090. After that basic setup screens will be there. We just need to go through them.

![Image](https://github.com/user-attachments/assets/f9476234-57f4-4ca4-a5ad-6c7a20dd81fd)

After going through the whole process. The initial homepage looks like this.
