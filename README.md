
# Set up EC2 and configure Python environment

This is a step-by-step tutorial of how to set up a Python environment for EC2 server.


## 1. Sign In
You can either access through root user or through IAM role. For users just signed up, we can only login through as root user by clicking "Sign in using root user email" below:

![alt text](imgs/aws1_tut_markdown.010.jpeg)


Choose "Root user", enter email and hit next.


![alt text](imgs/aws1_tut_markdown.011.jpeg)


Finally, hit "Sign in".

![alt text](imgs/aws1_tut_markdown.012.jpeg)


## 2. Create first AWS EC2 instance

After signed in, choose "Service", then click "All services"

![alt text](imgs/aws1_tut_markdown.014.jpeg)


Select "EC2" to enter EC2 dashboard.

![alt text](imgs/aws1_tut_markdown.015.jpeg)


Before launching an instance, you need to make sure the service location is correct. Here, I choose "Singapore" as the server's location. You need to make sure the server is close to you or your customers. After that, you can click "Launch instance" to start configuring an server instance.

![alt text](imgs/aws1_tut_markdown.016.jpeg)


Here, I named the instance as "my_linux_server". Then, I choose the operating system, and here I used Ubuntu (linux server).

![alt text](imgs/aws1_tut_markdown.017.jpeg)


To be specific, as a starter, you can select the version of "Ubuntu Server 24.04 LTS (HVM)". Moreover, the architecture is "64-bit (x86)". For free-tier The instance type should be "t2.micro".

![alt text](imgs/aws1_tut_markdown.018.jpeg)


Since we need to remote connect to the machine, we need to create a key pair to establish secure connection by clicking on the "create new key pair" button.

![alt text](imgs/aws1_tut_markdown.019.jpeg)

The key pair generates a public key and a private key. You need to give the key pair a name. For example, here I choose "aws_linux_server". I choose the RDS algorithm for encryption. Since I am a Mac user, I choose the key file format as ".pem". For Windows user, ".ppk" format is preferred. After all the configuration, click "Create key pair", and the browser will download your private key to your machine.

![alt text](imgs/aws1_tut_markdown.020.jpeg)


We need to set up the network settings. We need to allow ssh traffic. Furthermore, since we may establish a server or an application, we would just allow HTTP/HTTPS traffic from the internet.

![alt text](imgs/aws1_tut_markdown.021.jpeg)


Finally, we need to set up the storage to 30 GBs as shown below. This is the maximum allowed storage of the free-tier. Finally, there is a summary on the right hand side of the website. After making sure that everything is correct, click "Launch instance".

![alt text](imgs/aws1_tut_markdown.022.jpeg)


It won't take more than several minutes for AWS to get everything ready. 

![alt text](imgs/aws1_tut_markdown.023.jpeg)


As mentioned, you can always find any service by clicking "Services" button on upper left. This time, we can find EC2 service by clicking "Recently visited" and then click "EC2". 

![alt text](imgs/aws1_tut_markdown.024.jpeg)

After clicking "EC2", we arrived at a status dashboard of the EC2 service. On the right hand side shows your remaining time for free tier services. We can click on the "Instances (running)" to check our running services.

![alt text](imgs/aws1_tut_markdown.025.jpeg)


We arrive at a page listing all running EC2 instances. We can click on the specific Instance ID to look at information about the corresponding instance.

![alt text](imgs/aws1_tut_markdown.026.jpeg)

After we launch the page for the instance, let's click "Connect" button since we want to connect to the machine.

![alt text](imgs/aws1_tut_markdown.027.jpeg)

There are different ways to connect the EC2 instance. One easy way is to connect within the browser by selecting "EC2 Instance Connect" and then click on "Connect".

![alt text](imgs/aws1_tut_markdown.028.jpeg)


A new tab is established with the black terminal screen as shown below. The upper part summarizes the status of the machine, whereas the lower part allow one to text commands into the server.

![alt text](imgs/aws1_tut_markdown.029.jpeg)


A more professional way to connect is to use "SSH client" by clicking that option. Then, we can see a step-by-step guide of the establishing an SSH connection.

![alt text](imgs/aws1_tut_markdown.030.jpeg)


On your local machine, you can turn on your preferred command line tool like the Terminal in Mac or the Powershell in Win. Following the tutorial from the last image, we first run the "chmod 400" command to change to permission level for security reason. Then, we run the "ssh" command to establish the connection. If asked about wether to continue, type "yes" in the command line and hit enter to continue.

![alt text](imgs/aws1_tut_markdown.031.jpeg)


And now we just established a connection to the instance.

![alt text](imgs/aws1_tut_markdown.032.jpeg)


You can just type Linux commands you know. For example, "pwd" for passwords. "exit" to log out and end the connection.

![alt text](imgs/aws1_tut_markdown.033.jpeg)

## 3. Set up Python environment

Let's login again using ssh command to set up the remote server. First, we just update the related packages using the command "sudo apt update" and "sudo apt-get update".

![alt text](imgs/aws1_tut_markdown.034.jpeg)

Then, we install the latest python version from "apt-get" using the following command. Choose "Y" to continue.

![alt text](imgs/aws1_tut_markdown.035.jpeg)


Type "python3" to enter python page. We can now see that the python version is updated.


![alt text](imgs/aws1_tut_markdown.036.jpeg)

Run the command `python3 -m venv venv` to run the "venv" module to create a new environment called "venv" in a new folder called "venv". The environment is "virtual", meaning that we can activate it or deactivate it, and all the code in within the "venv" folder.

![alt text](imgs/aws1_tut_markdown.037.jpeg)

## 4. Set up Jupyter-lab server for remote access

We can use `source venv/bin/activate` to activate the virtual Python environment we just created. After that, we want to install jupyter-lab within the environment using `pip install jupyterlab`. We try to establish a Jupyter-lab server for our development.

![alt text](imgs/aws1_tut_markdown.038.jpeg)

Enter the command `jupyter-lab passwd` to create a password. This is necessary because only you should have access to the Jupyter-lab. Then we can start running the server using the command `jupyter-lab --ip='*' --port=8080 --no-browser`. After that, we can see that the server is running and we can just close this terminal.

![alt text](imgs/aws1_tut_markdown.039.jpeg)


Finally, we need to settle the network configuration to expose the portal of 8080 to the network. At the instance page, scroll down the select "Security", and then click on the "Security groups" to set up the "firewall" in AWS.

![alt text](imgs/aws1_tut_markdown.041.jpeg)

Click on "Edit inbound rules".

![alt text](imgs/aws1_tut_markdown.042.jpeg)


Add a new rule by clicking "Add rule" on bottom left. Then, set up the type as "Custom TCP". Set the port range to 8080. You can set up the source to any. Otherwise, you can use your own IP address if you don't change IP address frequently. After all settings, click "Save rules" to save results.

![alt text](imgs/aws1_tut_markdown.043.jpeg)

We can find the public IPv4 address from the instance page to access it.
![alt text](imgs/aws1_tut_markdown.040.jpeg)

For example, here that IP address is `13.229.201.20`. Thus, we can visit Jupyter-lab using the command `13.229.201.20:8080/lab`. After entering the password, you can see that we sucessfully "entered" the remote machine using Jupyter-lab.
![alt text](imgs/aws1_tut_markdown.044.jpeg)

![alt text](imgs/aws1_tut_markdown.045.jpeg)



It is also easy to stop the server. After SSH into the remote EC2, we can enter `jupyter-lab list` to see all running servers. we can run `jupyter-lab stop` to stop the server.

![alt text](imgs/aws1_tut_markdown.046.jpeg)


## 5. Use Visio Studio Code to SSH the EC2 server

Another way of using Python in remote machine is by connecting using the VS Code editor by installing the extention called "Remote - SSH". You need to enable this extention.

![alt text](imgs/aws1_tut_markdown.047.jpeg)


You can click on the bottom left blue bottom. After that, you can see a command pallate. Click on "Connect to Host...".

![alt text](imgs/aws1_tut_markdown.048.jpeg)


Then, click on "Add New SSH Host...". Here you can just type in the ssh command (recall that you can find that command from the AWS website).
![alt text](imgs/aws1_tut_markdown.049.jpeg)

![alt text](imgs/aws1_tut_markdown.050.jpeg)

In the command pallate, click on "Configure SSH Hosts..." to further configure the information.

![alt text](imgs/aws1_tut_markdown.051.jpeg)


A file in the path `.ssh/config` is opened. In the terminal, I used the command `cp aws_linux_server.pem ~/.ssh` to copy the file to the ".ssh" folder. I also changed the "IdentifyFile" filed to the new directory of the key file.

![alt text](imgs/aws1_tut_markdown.052.jpeg)

After that we can click this command instead of entering ssh command everytime.

![alt text](imgs/aws1_tut_markdown.053.jpeg)


Notice that after a connection is built, the blue part on the lower left changed.

![alt text](imgs/aws1_tut_markdown.054.jpeg)



If we open terminal, we can see that the terminal is also ssh connected.
![alt text](imgs/aws1_tut_markdown.055.jpeg)


## Close and manage instance

Let's close our instance to avoid unexpected fees for now. Click on "Instances (running)" to view all running instances. 

![alt text](imgs/aws1_tut_markdown.056.jpeg)

We can click on instance state to stop instance, reboot instance, and terminate (delete) instance.

![alt text](imgs/aws1_tut_markdown.057.jpeg)


Another thing is to generate an alert message if costs are generated. We can do this by clicking on the user name, and then on "Billing and Cost Management". 
![alt text](imgs/aws1_tut_markdown.058.jpeg)

Find Budgets on the left, then click on "Create Budget" to create an usage alert. There are some default templates to help you create such alerts.

![alt text](imgs/aws1_tut_markdown.059.jpeg)

