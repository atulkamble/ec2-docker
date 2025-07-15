# 📦 Docker on EC2 Instance — Setup & NGINX Container Run

This guide walks through creating an EC2 instance, installing Docker, pulling an image from Docker Hub, and running a container.

---

## 🚀 1️⃣ Launch EC2 Instance

* Go to AWS Management Console → EC2 Dashboard → **Launch Instance**
* Choose:

  * **AMI**: Amazon Linux 2 AMI
  * **Instance Type**: `t2.micro` (Free tier eligible)
  * **Key Pair**: `docker.pem` (download and save securely)
  * **Security Group**:

    * Allow **SSH (22)**
    * Allow **HTTP (80)**
* Launch the instance.

---

## 🔐 2️⃣ Connect to EC2 Instance

From your local terminal:

```bash
cd ~/Downloads
chmod 400 docker.pem
ssh -i "docker.pem" ec2-user@<your-ec2-public-dns>
```

Example:

```bash
ssh -i "docker.pem" ec2-user@ec2-54-152-7-36.compute-1.amazonaws.com
```

---

## ⚙️ 3️⃣ Install & Start Docker

On the EC2 instance, either via the **Advanced > User data** field while launching, or manually via SSH:

### Option A: Using User Data (during instance creation)

In **Advanced Details > User Data**:

```bash
#!/bin/bash
yum update -y
yum install docker -y
systemctl start docker
systemctl enable docker
```

### Option B: SSH in and run manually

```bash
sudo yum update -y
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
```

---

## 📜 4️⃣ Verify Docker Installation

```bash
docker --version
```

---

## 🐳 5️⃣ Pull an Image from Docker Hub

Go to [Docker Hub](https://hub.docker.com/), create a free account if you don't have one — recommended username format: `firstnameLastname`.

Then, on your EC2 instance:

```bash
sudo docker pull nginx
```

---

## 📦 6️⃣ List Downloaded Docker Images

```bash
sudo docker images
```

---

## ▶️ 7️⃣ Run an NGINX Docker Container

**Simple Run (foreground)**

```bash
sudo docker run nginx
```

**Detached Run with Port Mapping**

```bash
sudo docker run -d -p 80:80 nginx
```

---

## 📄 8️⃣ View Running Containers

```bash
sudo docker ps
```

---

## 📑 9️⃣ Check Container Logs

To check logs of a specific container:

```bash
sudo docker logs <container-id>
```

Example:

```bash
sudo docker logs fb14e
```

---

## 📖 1️⃣0️⃣ Helpful Commands Recap

```bash
clear                       # clear terminal
docker --version            # check Docker version
sudo docker images          # list images
sudo docker ps              # list running containers
sudo docker logs <id>       # view container logs
history                     # view command history
```

---

## ✅ 1️⃣1️⃣ Test Access

Open your browser and visit:

```
http://<your-ec2-public-ip>
```

You should see the default **Welcome to nginx!** page.

---

## 📓 Notes

* Always open **port 80** in your EC2 Security Group to access NGINX externally.
* Use `sudo docker stop <container-id>` to stop a running container.
* Use `sudo docker rm <container-id>` to remove a container.

---
## 👨‍💻 Author

**Atul Kamble**

- 💼 [LinkedIn](https://www.linkedin.com/in/atuljkamble)
- 🐙 [GitHub](https://github.com/atulkamble)
- 🐦 [X](https://x.com/Atul_Kamble)
- 📷 [Instagram](https://www.instagram.com/atuljkamble)
- 🌐 [Website](https://www.atulkamble.in)

