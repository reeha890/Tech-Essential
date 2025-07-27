**LAB : Deploying an Enterprise Web**

I’ll create virtual servers, install WordPress, configure security, and even build in high availability using load balancing and auto scaling. Let’s break it down

**Step 1**: Building Your Cloud Environment
🔹 1. Create a VPC (Virtual Private Cloud)
Think of a VPC as your private network on the cloud. It’s like your own secure neighborhood where your cloud servers live. In this step, you create one and choose the AP-Singapore region (or any closest to your users).

🔹 2. Set Up Security Rules
Next, you build a security group—a kind of firewall. You allow traffic from anywhere (0.0.0.0/0) for testing, but in real-world setups, you’d want to be more strict for safety.

![2](https://github.com/user-attachments/assets/eeb74f9a-9aa6-4600-93c8-8d6074e992a0)


 **Step 2**: Launching the Servers
🔹 3. Create an ECS (Elastic Cloud Server)
This is your actual web server. You pick CentOS as the operating system and give it basic specs like 1 vCPU and 1GB RAM. You assign it an IP address so you can access it from the internet.

🔹 4. Add a Database (RDS)
Websites like WordPress need databases. Huawei Cloud offers Relational Database Service (RDS)—a managed MySQL database that you can easily deploy. No need to worry about backups or maintenance—Huawei handles that.

**Step 3**: Setting Up the LAMP Stack
Now that your server is up, it’s time to install the LAMP stack:
Linux (already installed)
Apache (web server)
MySQL (database)
PHP (for dynamic content)
You log into your server, install everything with a simple command, and configure Apache to start automatically. You also download and extract WordPress, which is the website software you'll be running.

**Step 4**: Connecting WordPress to the Database
After installing WordPress, you:
Create a new database called wordpress using the RDS console.
Access your server’s IP in a browser and launch the WordPress installation wizard.
Input the database details (like username, password, IP).
Set your site title, admin account, and boom—you’re live!

**Step 5**: Make Your Website Scalable & Reliable
🔹 Use a Load Balancer (ELB)
A load balancer spreads traffic across multiple servers. That way, if one server is overloaded or fails, another picks up the slack.
 Create a System Image
You take a snapshot of your configured server so you can clone it when needed—like making copies of a well-decorated room.
 Set Up Auto Scaling (AS)
With auto scaling, Huawei Cloud automatically adds or removes servers based on traffic. For example:
If CPU usage > 60%, add 1 server.
If CPU usage < 20%, remove 1 server.
It’s like having a smart system that adjusts resources depending on how many customers are visiting your site.

 **Step 6**: Visit Your Website
Access the load balancer’s public IP and see your WordPress site live on the internet. Thanks to ELB and AS, your site can now handle more users and stay online even during traffic surges.

 **Step 7**: Monitor Your Resources
Head to Cloud Eye, Huawei’s monitoring tool:
View server performance
Track alarms and issues
Get real-time stats on CPU, memory, and network

![1](https://github.com/user-attachments/assets/712e8daf-c364-4a5a-a28f-a06f081bc3bf)
