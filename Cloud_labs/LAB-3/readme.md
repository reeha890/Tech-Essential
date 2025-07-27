LAB: Deployment of compute service

**Step 1**: Creating Your Virtual Machines (ECS)
💡 What’s an ECS?
Think of an ECS as your computer—but it's online, inside a powerful data center. You can choose the operating system, the amount of CPU and memory, and even its "neighborhood" (called a VPC, or Virtual Private Cloud).

🖥️ Create a Windows ECS
Log into the Huawei Cloud Console using your lab account.

Create a VPC with the IP range 192.168.0.0/16 and a subnet 192.168.0.0/24.

From the Compute > Elastic Cloud Server section, click Buy ECS.

Choose:

Billing: Pay-per-use

Specs: 2 vCPUs, 4 GB RAM

OS: Windows Server 2012 R2

Disk: 40GB, High I/O

Security: Basic enabled

Set the name (e.g., ecs-windows) and a password like Huawei@1234.

Confirm and submit!

🐧 Now Create a Linux ECS
Do the same steps again, but this time:

OS: CentOS 7.6

Name: ecs-linux

And for network, enable public access (EIP) so you can connect via SSH later if needed.

![6](https://github.com/user-attachments/assets/9943f4ed-8028-4429-a3de-e8d2d1622512)


 **Step 2**: Logging Into Your ECS
You’ve created the ECSs, now let’s access them.

🔐 Windows ECS
Go to your ECS list, click Remote Login, then Log In.

Click "Send Ctrl+Alt+Delete" to get the login screen.

Paste your password and hit Enter—boom, you're in!
 Linux ECS
Since Linux doesn’t have a desktop GUI here, you’ll use a text-based interface.

Use Remote Login (VNC) and log in with:

Username: root

Password: Your set password (e.g., Huawei@123)

If you see "Welcome to Huawei Cloud Service"—you did it!

**Step 3**: Changing ECS Specifications (Upgrading Your Server)
Let’s say your Windows ECS needs more memory:

Stop the ECS.

Click More > Modify Specifications.

Change from 4 GB to 8 GB memory.

Submit and restart.

That’s it—your cloud PC just got a RAM upgrade!

 **Step 4**: Creating a Custom Image (Template)
You might want to reuse your configured ECS for future use—without starting from scratch. You can create a private image, which acts like a reusable template.

🪟 For Windows ECS:
Make sure the ECS is configured (e.g., DHCP enabled, Remote Desktop allowed).

Go to Image Management Service > Create Image.

Choose your ECS, give the image a name like image-windows2012, and submit.

Wait 10–20 mins for it to be ready.

Now you have a reusable image with your settings baked in!

 For Linux ECS:
Same concept, but check a few more things:

DHCP is enabled (you may edit /etc/sysconfig/network-scripts/ifcfg-eth0)

Make sure Cloud-Init is installed (use rpm -qa | grep cloud-init)

Optional but recommended: ensure the one-click password reset plugin is installed

Then:

Go to Image Management > Create Image

Choose ecs-linux, name it something like image-centos7.6

Submit and wait!

![7](https://github.com/user-attachments/assets/19d5725f-74c6-4eeb-88ab-a983de111c2e)


 **Step 5**: Using and Sharing Images
 Reusing Your Image
Want to launch a new ECS using your saved template?

Go to your image

Click Apply for Server

Launch an ECS from it—it’ll have all your settings/software preinstalled!
Sharing Images with Others
Get their Project ID (found under “My Credentials” in their Huawei account).
In your image panel, click Share > Add Project ID.
That user will now see the image under Shared Images and can accept it.
Perfect for teams or collaborative labs.
