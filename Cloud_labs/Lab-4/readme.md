LAB: Deploy a Networks & STORAGE SERVICE ON HUAWEI CLOUD

Steps to Deploy Network Services on Huawei Cloud:
**Step1**. Create a VPC (Virtual Private Cloud)
A VPC is like a private network room in the cloud. You get to define the IP range and who gets access.

Go to Service List > Networking > VPC

Click Create VPC

Set:

Name: vpc-network

CIDR Block: 192.168.0.0/16

Add a subnet (like a small street in your neighborhood)

Name: subnet-web

CIDR Block: 192.168.1.0/24

**Step2**. Configure a Security Group
Think of this as your virtual firewall.

Navigate to Access Control > Security Groups

Add rules like:

Allow HTTP (port 80) for web traffic

Allow SSH (port 22) for secure remote access

**Step3**. Assign Elastic IPs (EIP)
These give your cloud servers public internet access.

Go to Elastic IP > Apply for EIP

Assign it to your server or load balancer

**Step4**. Use Elastic Load Balancer (ELB)
Want your app to stay online even under heavy traffic? Use an ELB to spread user traffic across multiple servers.

Navigate to Networking > Elastic Load Balance

Create a Shared Load Balancer

Link it to your VPC and backend servers

Enable Health Checks to monitor server status

![8](https://github.com/user-attachments/assets/d3e02214-1bcb-4cab-9a14-2d62c21eedf9)


 **PART 2**: STORAGE SERVICES – Where Your Data Lives
💡 Why Is Cloud Storage Important?
In the cloud, everything is virtual—but it still needs to be stored somewhere! Whether it's web content, databases, or backups, Huawei offers flexible and scalable options for storage.

🧰 Huawei Cloud Storage Options:
**Step1**. EVS (Elastic Volume Service) – Like a Hard Drive for Your ECS
Each ECS (virtual server) gets a system disk (OS) and optional data disks

Go to Elastic Volume Service > Create Disk

Choose:

Type: SSD (for speed) or SATA (for cost-efficiency)

Size: e.g., 100 GB

Attach it to your ECS and format it from within the server

**Step2**. OBS (Object Storage Service) – Like Google Drive but for apps
Perfect for storing:

Images

Backups

Videos

Static website files

Steps:

Go to OBS > Create Bucket

Set:

Bucket Name: my-media-bucket

Region: AP-Singapore (or closest to your users)

Upload files or configure it as a static website host

![9](https://github.com/user-attachments/assets/99f43e40-ae08-4785-b4bd-7c3054758922)

**Step3**. SFS (Scalable File Service) – Shared file system
If multiple ECSs need to read/write the same data, SFS acts like a shared folder they all connect to.

🛡️ BONUS: Storage Security & Backup
Use Cloud Backup and Recovery for scheduled snapshots of your disks

Encrypt OBS buckets for sensitive data

Use IAM roles to control who can access which storage
