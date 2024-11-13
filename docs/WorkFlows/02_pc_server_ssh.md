# PC-Server SSH Connection Setup

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/workflows/triton.jpg?raw=true" alt="triton" width="300" height="300">
</div>

## **Prerequisites**

  - A **server**, in this case, Ubuntu 24 connected to the router through an Ethernet cable with IP *192.168.1.10*.
  - A **PC**, in this case, a Windows 11 laptop connected via Wi-Fi to the router, with IP *192.168.1.20*.
  - Basic **command-line skills**.

## **Objective**

Establish a secure connection to manage the server through the Personal Computer.

---

## **Prologue: Triton’s Mission**

King Triton, ruler of the Seven Seas, has decreed that his daughter’s private room—the Little Mermaid's chamber—be secured from intruders, especially meddling land-dwellers! To achieve this, he’s decided to set up a magical barrier that only his trusted trident can unlock. He must configure the chamber’s underwater server to recognize his trident’s unique signal while denying entry to all others. With these steps, Triton will secure the chamber and keep the treasures safe.

---

## **On the Server: Preparing the Little Mermaid’s Chamber**

1. **Command the Ocean Currents (Install SSH)**
   First, Triton must install and activate the secure SSH protocol on the server, so it responds to his trident’s signal.
   ```bash
   sudo apt update
   sudo apt install openssh-server
   sudo systemctl enable ssh
   sudo systemctl start ssh
   ```

2. **Summon a Protective Sea Barrier (UFW Firewall)**
   Using his power, Triton establishes a firewall, granting only his trident’s unique signal the right to pass. Any other sea creatures or land-dwellers will be blocked from entry.
   - Replace `192.168.1.20` with the IP address of Triton’s trident.
   ```bash
   sudo ufw allow from 192.168.1.20 to any port 22   # Allow only Triton’s trident IP
   sudo ufw deny 22                                  # Block all other IPs
   sudo ufw enable                                   # Raise the sea barrier
   ```

3. **Engrave an Access Inscription on the Chamber**
   Triton engraves an inscription on the server, specifying that only his trident’s IP address is allowed entry into the chamber.
   - Replace `username` with Triton’s undersea server username, more details at the bottom, and `192.168.1.20` with his trident’s IP address.
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
   Add:
   ```plaintext
   AllowUsers username@192.168.1.20
   ```
   **Restart SSH** to apply these changes, so the chamber only opens to Triton’s trident.
   ```bash
   sudo systemctl restart ssh
   ```

4. **Forge a Golden Key for Entry (Optional)**
   As an extra layer of protection, Triton creates a unique key to grant his trident safe passage. This key ensures only his signal, and no one else’s, can enter the Little Mermaid’s chamber.
   ```bash
   ssh-copy-id username@192.168.1.10   # Replace with server username and IP
   ```

5. **Seal the Chamber Against All Passwords**
   Triton, a wise king, knows that passwords can be guessed by those with dark intentions. He seals the chamber so only those with his key can enter.
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
   Set:
   ```plaintext
   PasswordAuthentication no
   ```
   **Restart SSH** for the final layer of magical protection:
   ```bash
   sudo systemctl restart ssh
   ```

---

## **On the Personal computer: Prepare to Unlock the Chamber with the Trident**

1. **Create the Golden Key**
   If not already forged, Triton creates a unique SSH key for his trident. This key will serve as his enchanted ticket to the chamber.
   ```bash
   ssh-keygen -t rsa -b 4096
   ```
   - Accept the default location (`~/.ssh/id_rsa`) by pressing **Enter** and set a passphrase to keep the key safe.

2. **Transfer the Key to the Server Chamber**
   With his golden key ready, Triton transfers it to the server so it recognizes his trident upon approach.
   ```bash
   ssh-copy-id username@192.168.1.10   # Replace with server IP
   ```

3. **Command the Seas to Open**
   With all the protections in place, Triton finally connects to the server, confident in his secure access to the Little Mermaid’s chamber.
   ```bash
   ssh username@192.168.1.10
   ```

---

## **Commands Recap: Triton’s Magical Compendium**

Here’s a quick scroll of all the commands, ensuring that the chamber remains sealed to all but Triton’s trident:

### **Commands for the Little Mermaid's Server Chamber**
```bash
# Install and start SSH server on the chamber
sudo apt update
sudo apt install openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh

# Setup firewall to restrict access to only Triton’s IP
sudo ufw allow from 192.168.1.20 to any port 22   # Allow only Triton’s trident IP
sudo ufw deny 22                                  # Block all other IPs
sudo ufw enable                                   # Activate the firewall

# Restrict SSH access to only Triton’s trident
sudo nano /etc/ssh/sshd_config                    # Edit SSH config file
# Add: AllowUsers username@192.168.1.20
sudo systemctl restart ssh                        # Restart SSH

# Optional: Disable password authentication after setting up SSH keys
sudo nano /etc/ssh/sshd_config                    # Edit SSH config file
# Set: PasswordAuthentication no
sudo systemctl restart ssh                        # Restart SSH
```

### **Commands for Triton’s Trident**
```bash
# Generate SSH keys if not done already
ssh-keygen -t rsa -b 4096

# Transfer SSH key to the chamber for access
ssh-copy-id username@192.168.1.10                 # Replace with server IP

# Connect to the chamber securely
ssh username@192.168.1.10                         # Replace with server IP
```

---

## Username deep dive:

In this guide, the **`username`** part refers to the specific **user account** that you create or use to access your server. When you're setting up an SSH connection, the username tells the server which account you're attempting to log into.

1. **Server-side configuration (Triton's Chamber)**:
   - When you modify the SSH configuration to restrict access, you will define the `username` on the server who can connect.
   - For example, if you have a user called `triton` on your server, you would set it like this in the SSH configuration file (`/etc/ssh/sshd_config`):
     ```plaintext
     AllowUsers triton@192.168.1.20
     ```
     This means that only the user `triton` from IP `192.168.1.20` is allowed to connect to the server. Any other users or IPs will be denied.

2. **Laptop-side configuration (Trident's Device)**:
   - On your laptop (Trident), you use the **username** to tell the SSH client which user account on the server to log in as.
   - For example, when using the `ssh` command to connect:
     ```bash
     ssh triton@192.168.1.10
     ```
     Here, `triton` is the **username** on the server, and `192.168.1.10` is the **server's IP address**.
   - This will attempt to log into the server as the `triton` user.

### Username importance
- The **username** is essential because it allows the SSH system to identify the correct user on the server and grant access based on the associated permissions.
- It also helps in managing who can access the server. You can set up specific permissions for different users or groups of users.

### A practical example:

- **On the Server**: Let's say you have a server (the Little Mermaid's chamber) with a user called `triton`:
  ```bash
  sudo adduser triton
  ```
- **On the Laptop**: To connect to the server using the username `triton`, you run:
  ```bash
  ssh triton@192.168.1.10
  ```

This tells the server, "Log me in as the `triton` user from this laptop." If `triton` has SSH access (because of the configuration in `/etc/ssh/sshd_config`), you'll be granted access. If not, the connection will be denied.


### Key Takeaway:
The **username** is the account you’re using to authenticate and connect to the server. It’s important to replace `username` with the actual user on the server (like `triton` or any other user you have set up on your system).


---

## **Making sure machines are assigned Static IPs from the Router**

To ensure that only Triton’s trusted trident (laptop) can reach the Little Mermaid’s chamber (server), King Triton uses the magical router to assign **static IPs** to both devices. This ensures their positions in the network are fixed.

### **Steps to Assign Static IPs:**

1. **Enter the Router’s Domain**:
   Triton navigates to the router’s web interface (usually `192.168.1.1`,  `192.168.0.1` or `192.168.1.254`) and logs in with the router’s credentials.

2. **Find DHCP Settings**:
   Triton searches for the **DHCP Reservation** or **Static IP Binding** section to bind devices to fixed IPs.

3. **Gather MAC Addresses**:
   - **Server**: Run `ip link` in the terminal to find the server’s MAC address.
   - **Laptop**: Run `ipconfig /all` in Command Prompt to find the laptop’s MAC address.

4. **Bind Devices to Static IPs**:
   - Enter the **MAC address** and assign IPs like `192.168.1.10` for the server and `192.168.1.20` for the laptop.

5. **Apply Changes**:
   Triton saves the settings and restarts the router if necessary. The devices are now fixed at their IPs, ensuring they always return to their assigned locations.

6. **Verify**:
   - **Server**: Run `ip a` to check the IP.
   - **Laptop**: Run `ipconfig` to verify the IP.

Now, with Triton’s IP commands in place, the devices are securely anchored to their IPs, ensuring a reliable connection to manage the Little Mermaid's chamber.

---

## **Epilogue: Triton’s Legacy**

With his server properly secured, Triton can rest assured knowing that only his trident will unlock the doors to the Little Mermaid’s chamber. The ocean remains safe, with no land-dwellers or intruders able to enter his protected kingdom. The treasures in the Little Mermaid’s chamber are safeguarded, and her father’s watchful magic guards the seas.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>