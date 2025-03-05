# ssh-ufw

To set up a firewall on your Ubuntu server with the specified rules, you can use ufw (Uncomplicated Firewall), which is a user-friendly interface for managing iptables. Below are the steps to configure the firewall according to your requirements:

# Step 1: Install ufw (if not already installed)
```
Copy
sudo apt update
sudo apt install ufw
```
# Step 2: Set Default Policies
Set the default policies to deny all incoming and allow all outgoing traffic:

```
sudo ufw default deny incoming
sudo ufw default allow outgoing
```
# Step 3: Allow Traffic from 103.68.104.0/24 to All Ports
Allow all traffic from the 103.68.104.0/24 subnet to your server:
```
sudo ufw allow from 103.68.104.0/24 to any
```
# Step 4: Block Port 62025 for All Except 103.68.104.0/24
First, allow port 62025 for the 103.68.104.0/24 subnet:

```
sudo ufw allow from 103.68.104.0/24 to any port 62025

```
Then, block port 62025 for all other IPs:

```
sudo ufw deny 62025
```

# Step 5: Allow Port 80 for All
Allow port 80 (HTTP) for all users:
```
sudo ufw allow 80/tcp
```
# Step 6: Enable the Firewall
After configuring the rules, enable the firewall:
```
sudo ufw enable
```
# Step 7: Verify the Rules
Check the status of the firewall to ensure the rules are correctly applied:

```
sudo ufw status verbose
```
Example Output:
```
Status: active

To                         Action      From
--                         ------      ----
Anywhere                   ALLOW       103.68.104.0/24
62025                      ALLOW       103.68.104.0/24
80/tcp                     ALLOW       Anywhere
62025                      DENY        Anywhere
```
# Step 8: (Optional) Allow SSH Access
If you are managing the server remotely, ensure that SSH (port 22) is allowed:

```
sudo ufw allow 22/tcp
```
Step 9: (Optional) Reload the Firewall
If you make any changes, you can reload the firewall:
```
sudo ufw reload
```

Summary
All traffic from 103.68.104.0/24 is allowed to any port.

Port 62025 is blocked for all except 103.68.104.0/24.

Port 80 is open for all users.

The firewall is enabled and active.

This configuration should meet your requirements. Make sure to test the rules to ensure they are working as expected.

