# Hosting a Python Telegram Bot Without Webhooks GUIDE

<div align="center">
  <a href="https://github.com/arhkypGitProject" target="_blank">
    <img src="https://img.shields.io/static/v1?message=GitHub&logo=github&label=&color=181717&logoColor=white&style=for-the-badge" height="25" />
  </a>
</div>

<div align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=arhkypGitProject.Hosting-a-Python-Telegram-Bot-Without-Webhooks" />
</div>

<div align="center">
  <img src="https://skillicons.dev/icons?i=python" height="20" /> Python / Aiogram
</div>


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

<b>After locating your bot's folder, it is time to connect to the VPS server using FileZilla.

### Before connecting, it is recommended to close the console session that was used for the previous SSH connection.</b>

<b>At the top of the FileZilla window, you will see the following fields: **Host**, **Username**, **Password**, and **Port**.

Fill in these fields as follows:

- **Host** — Enter the IP address of your VPS server.
- **Username** — Enter `root` (**important: use lowercase letters**).
- **Password** — Enter your root password from the VPS server information page.
- **Port** — This field is important. In some cases, the port is not provided by the hosting provider. The standard SSH port is usually `22` (sometimes `21` is used for FTP, but for SSH connections it is almost always `22`).

After filling in all the fields, click **Quickconnect** and wait for the connection to be established.

On the right side, you should see the **root** folder. This means that you have successfully connected to your VPS server.
</b>

<img width="1179" height="753" alt="изображение_2026-07-09_213649831-fotor-20260709214111" src="https://github.com/user-attachments/assets/ee77dd20-b07b-4dd1-8464-d4e1a26e2b1e" />

# Step 6: Uploading Bot Files to the VPS Server

<b>Select the folder that contains your bot's main directories and the startup file.

Right-click on the folder and choose **Upload** from the context menu to begin transferring the files to the VPS server.</b>

After the transfer is complete, the files should appear here:

<img width="1179" height="753" alt="изображение_2026-07-09_213649831-fotor-20260709214759" src="https://github.com/user-attachments/assets/d74af0cd-9157-41ac-9d59-041ff659340c" />

### After this, you can safely close FileZilla and return to the console.

# Step 7: Running the Bot on the VPS Server

<b>After uploading the files to the server using FileZilla, open the console and connect to the VPS server the same way as we did earlier in **Step 2**.</b>

First, check that your bot folder has been uploaded correctly by using the `ls` command:

```bash
ls
```

The output should look similar to this:

```bash
root@ServerName:~# ls
folder_bot
```

If you see your bot's folder name, it means that the files were uploaded successfully and you can continue with the next steps.

If everything is correct, enter the following command to open your bot's folder:

```bash
cd FOLDER_NAME
```

Replace `FOLDER_NAME` with the name of your bot's folder.

Example:

```bash
cd folder_bot
```

After running this command, you will be moved inside your bot's project directory.

After running the `cd` command, your terminal path should change to your bot's directory.

Example:

```bash
root@ServerName:~/folder_bot#
```

This means that you are now inside the bot's project folder and can continue with the next setup steps.

Next, run the following commands:


```bash

# Check the files in the current directory

ls



# Install all required Python dependencies

pip3 install -r requirements.txt



# Start the bot using PM2

pm2 start main.py --interpreter python3

```

Replace `main.py` with the name of your bot's main startup file if it has a different name.

After running these commands, your Telegram bot should start running on the VPS server.

To check if your bot process is running, use the following command:

```bash
pm2 list
```
If the bot is running successfully, you will see your process in the list with the status **online**.

Example:

```bash
┌────┬──────────────┬─────────┬────────┐
│ id │ name         │ status  │ mode   │
├────┼──────────────┼─────────┼────────┤
│ 0  │ main         │ online  │ fork   │
└────┴──────────────┴─────────┴────────┘
```
# Conclusion

That's it! Your Telegram bot is now successfully deployed and running on your VPS server.

You have completed all the necessary steps:
- Configured the VPS server
- Connected to the server via SSH
- Uploaded the bot files using FileZilla
- Installed the required dependencies
- Started the bot using PM2

Your bot should now be running continuously in the background.

## Support the Project ⭐

If this guide helped you deploy your Telegram bot, consider giving this repository a **star ⭐**.

Your support helps me stay motivated to create more useful guides, tutorials, and open-source projects.

Thank you for your support and for being part of this project! 🚀
