**LAB : Deploying DeepSeek on Huawei Cloud**

**Step 1**: Prepare Your Cloud Environment
Before anything else, you’ll need access to Huawei Cloud Lab Desktop using a provided lab account (not your personal one). Once logged in, you’ll create an Elastic Cloud Server (ECS).

![4](https://github.com/user-attachments/assets/2aa31dad-1f10-4e9b-8963-d130b81a7404)


Creating the ECS
Think of the ECS as your remote computer in the cloud. Here’s what you’ll configure:

Region: AP-Singapore

CPU & Memory: 4 vCPUs, 8GB RAM (good enough for DeepSeek 1.5B)

OS Image: CentOS 8.2 (64-bit)

Storage: 40GB

Bandwidth: 100 Mbit/s (very important for downloading models quickly)

Password: Huawei1234% (remember this—it’s your admin key)

After setting all of this, your virtual machine will be created. You'll now log into it via CloudShell, a browser-based terminal.

![5](https://github.com/user-attachments/assets/81e23fb0-c32a-40aa-a409-0ecf141acb2b)


 Step 2: Install Ollama (The LLM Manager)
Ollama is a powerful tool that makes it easy to install and run large language models like DeepSeek. You have two options to install it:

![3](https://github.com/user-attachments/assets/58ea1c17-223a-4bf2-b5ef-cba17af10a2e)


✅ Option 1: Install from GitHub
Run this in your terminal:

bash
Copy
Edit
curl -fsSL https://ollama.com/install.sh | sh
Then check it worked:

bash
Copy
Edit
ollama -v
⚡ Option 2: Install from Huawei Cloud (Faster)
If GitHub is slow or fails, use this method:

bash
Copy
Edit
wget https://sandbox-experiment-files.obs.cn-north-4.myhuaweicloud.com/deepseek/ollama-linux-amd64.tgz
sudo tar -C /usr -xzf ollama-linux-amd64.tgz
sudo chmod +x /usr/bin/ollama
Set up Ollama as a system service (so it runs in the background):

bash
Copy
Edit
sudo useradd -r -s /bin/false -m -d /usr/share/ollama ollama
Create and enable the systemd service:

bash
Copy
Edit
# Create ollama.service file
cat << EOF | sudo tee /etc/systemd/system/ollama.service
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
ExecStart=/usr/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3

[Install]
WantedBy=default.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable ollama
sudo systemctl start ollama
Now verify it’s up:

bash
Copy
Edit
ollama -v
Awesome! You now have a working Ollama server on your Huawei ECS.

 Step 3: Deploy DeepSeek-R1 1.5B
Now comes the exciting part—running the DeepSeek LLM!

🧪 Option 1: Pull DeepSeek Model from Ollama
This will take time depending on your connection:

bash
Copy
Edit
ollama pull deepseek-r1:1.5b
Then launch it:

bash
Copy
Edit
ollama run deepseek-r1:1.5b
🚀 Option 2: Download from Huawei OBS (Faster & Reliable)
Download the model:

bash
Copy
Edit
wget https://sandbox-experiment-files.obs.cn-north-4.myhuaweicloud.com/deepseek/ollama_deepseek_r1_1.5b.tar.gz
Extract the model into Ollama’s directory:

bash
Copy
Edit
sudo tar -C /usr/share/ollama/.ollama/models -xzf ollama_deepseek_r1_1.5b.tar.gz
Move the files into the correct folders:

bash
Copy
Edit
cd /usr/share/ollama/.ollama/models
mv ./deepseek/sha256* ./blobs
mkdir -p ./manifests/registry.ollama.ai/library/deepseek-r1
mv ./deepseek/1.5b ./manifests/registry.ollama.ai/library/deepseek-r1
rm -rf deepseek/
Check if DeepSeek is ready:

bash
Copy
Edit
ollama list
Run the model:

bash
Copy
Edit
ollama run deepseek-r1:1.5b
