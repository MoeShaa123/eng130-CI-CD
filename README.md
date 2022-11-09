# Jenkins/CI-CD

![jen drawio](https://user-images.githubusercontent.com/106158041/200811214-2754cfb9-0259-42a6-b68d-9db015477d8e.png)

## Connecting Jenkins with EC2 instance

![jenkins drawio](https://user-images.githubusercontent.com/106158041/200811268-190f7d5e-b407-42e1-865e-59cd2e08400a.png)

### In AWS

- Create a new EC2 instance
- Choose Ubuntu Server 16.04 LTS (HVM), SSD Volume Type as the AMI
- Choose t2.micro as the instance type (the default)
- Enter a suitable name and description for the Security Group with the following rules:
  - SSH (22) with source My IP - allows you to SSH
  - SSH (22) with source jenkins_server_ip/32 - allows Jenkins server to SSH
  - HTTP (80) with source Anywhere - allow access to the app
  - Custom TCP (3000) with source 0.0.0.0/0 - allow access to port 3000
- Review and Launch

### In Jenkins

- Select SSH Agent
- Select Specific credentials
- Use Repo URL from Dev Branch
- In the command shell run this code:

```
    rsync -avz -e "ssh -o StrictHostKeyChecking=no" app ubuntu@54.229.241.174:/home/ubuntu/app

    ssh -A -o "StrictHostKeyChecking=no" ubuntu@54.229.241.174 <<EOF
        cd app
        cd app
        killall npm
        nohup node app.js > /dev/null 2>&1 &
    EOF
```

- Make sure you have copied the app folder
- Now you should have the app running on port 3000
