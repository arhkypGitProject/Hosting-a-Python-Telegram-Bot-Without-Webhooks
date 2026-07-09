# Hosting a Python Telegram Bot Without Webhooks GUIDE
* Simple deployment of an Aiogram 3 Telegram bot on Ubuntu VPS (AdminVPS.ru)




<b>*Before we get started, I'd like to briefly explain which hosting provider I used and why.*

### Term Explanation

- **Command Prompt (CMD)** — a command-line interface built into Windows that allows users to execute commands and interact with the operating system using text commands.

- **SSH (Secure Shell)** — a network protocol that allows you to securely connect to and manage a remote server over an encrypted connection.

- **VPS (Virtual Private Server)** — a virtual machine hosted on a physical server that provides dedicated resources and full control over the operating system.

For this tutorial, I used *[AdminVPS.ru](https://adminvps.ru)*. I decided to record this guide while completing a real client project. The client purchased the VPS specifically to host and secure their Telegram bot.

For privacy and security reasons, all sensitive information—including the server IP address, credentials, domain names, and any details that could identify the client or their infrastructure—has been hidden throughout this tutorial. </b>

First, you'll need a VPS server. You can choose any hosting provider you prefer, as most VPS services are very similar and the deployment process is nearly identical across different providers.

In this guide, I'll be using *[AdminVPS.ru](https://adminvps.ru)*, but you're free to use any VPS hosting provider of your choice.

# Step 1: Initial VPS Server Setup After Purchase

<b>After opening the server management page, you will see information similar to this. It will contain your server IP address, the root password, and the available ports (sometimes ports are not displayed, as in my case).</b>

<img width="457" height="443" alt="image" src="https://github.com/user-attachments/assets/edcd1a69-fcec-4b49-9c98-fe26155315b3" />

<b>The next step is to open your server console. In most cases, the console is already built into your hosting provider's dashboard. Look for a section called "Console", "Web Console", or a similar option.

However, in my case, I will use the built-in Windows Command Prompt (CMD) and connect to the VPS server through SSH.
The steps are the same regardless of which console you use.</b>

# Step 2: Console Setup and Remote Connection to the VPS Server

<b>Open the console provided by your hosting provider, or open Windows Command Prompt (CMD) as Administrator, as I will do in this guide.</b>

## Connecting to the VPS Server Using CMD

You will see a command line window like this.

<img width="959" height="434" alt="image" src="https://github.com/user-attachments/assets/edbf4b3c-7ac9-470e-978d-dae3b42d83bd" />

<b>To connect to the server remotely, we will use the `ssh` command.

Next, enter the following command into the command line:</b>

```bash
ssh root@YOUR_SERVER_IP_ADDRESS

```
The command should look something like this:

```bash
ssh root@185.221.160.4
```

## Using the Hosting Provider's Web Console

<b>In this case, the SSH connection will be established automatically. You do not need to enter the SSH command manually, unlike when using CMD.</b>

# Step 3: Logging In and Entering the Root Password

After entering the command through CMD or opening the web console, you will be prompted to enter the **root password**.

In my case, the password is available on the server information page, so I can simply **copy and paste** it into the console.

> **Important:** The paste shortcut is not the same in every console. On many Linux-based consoles, **Ctrl + V** does not work. Instead, paste the password by **right-clicking** inside the console window.

> **Note:** If the password is not visible while typing, this is completely normal. Linux does **not** display any characters (not even dots or asterisks) when entering a password. Simply type or paste the password and press **Enter**.

If the login still fails, try **typing the password manually** instead of copying and pasting it.

### <b>After entering the correct password, you should see output similar to the following:</b>

<img width="720" height="636" alt="image" src="https://github.com/user-attachments/assets/ad9fc180-1f16-46eb-903c-e415a0e63caa" />

# Step 4: Updating the System and Installing Python

<b>Run the following commands one by one to update your system and install the latest Python packages:</b>

```bash
# Update package lists
sudo apt update

# Upgrade installed packages
sudo apt upgrade -y

# Install Python and required tools
sudo apt install -y python3 python3-pip python3-venv

# Install Node.js and npm
sudo apt install -y nodejs npm

# Install PM2 globally
sudo npm install -g pm2

# Remove unnecessary packages
sudo apt autoremove -y

# Verify the installations
python3 --version
pip3 --version
node --version
npm --version
pm2 --version
```
# Step 5: Installing and Configuring FileZilla

<b>[FileZilla](https://filezilla-project.org) is an FTP/SFTP client that we will use to transfer our Telegram bot files from our local computer to the VPS server.

After installing FileZilla, launch the application. You will see a window similar to the one shown below:
</b>

<img width="1176" height="887" alt="image" src="https://github.com/user-attachments/assets/f4aca42a-bc81-4a05-89f9-985e791af267" />

Next, in the **Local Site** panel, either enter the path to your Telegram bot's project folder or use the built-in file browser to locate it manually.
