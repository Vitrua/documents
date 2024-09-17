# Windows to iOS File Transfer

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/ospace/winios.jpg?raw=true" alt="winios" width="300" height="300">
</div>

## Objective

Transfer files from a Windows PC to an iOS device in a safe and easy way using a shared folder.

## Prerequisites

- Windows PC
- iOS Device (iPhone or iPad)
- Both devices connected to the same Wi-Fi network

## Introduction

In a galaxy far away, Captain Stellar of the Starship Nimbus is on a crucial mission. She needs to send important star maps from her ship's main computer (running on Windows) to her portable exploration device (an iOS system) before her next jump to a new star system. The galactic communications network is down, so relying on third-party services is risky—her data could be intercepted by space pirates or rogue AIs.

To securely transfer the files, Captain Stellar knows she must use a shared folder, keeping her star maps within her control, even in the vastness of space.


## Steps

### Step 1: Create a Shared Folder on Windows

To keep the star maps safe, Captain Stellar first needs to create a secure folder on her onboard computer.

1. **Create a new folder:**
   - Open File Explorer on your Windows PC.
   - Navigate to the location where you want to create the shared folder (e.g., Desktop).
   - Right-click, select "New," and then click "Folder."
   - Name the folder (e.g., "SharedFiles").

2. **Set up sharing permissions:**
   - Right-click the folder you just created and select "Properties."
   - Go to the **Sharing** tab and click **Advanced Sharing**.
   - Check the box **Share this folder**.
   - Click the **Permissions** button, select the user account (usually "Everyone"), and set the desired permissions (e.g., "Read/Write" for full access or "Read" for view-only).
   - Click **OK** to confirm.

3. **Assign a specific account:**
   - Go back to the **Sharing** tab and click **Share**.
   - Choose a custom account (e.g., your own user account) or create a new local account for security.
   - Assign permission levels as needed (e.g., "Read/Write" or "Read").
   - Note the username and password associated with this account.

4. **Get the network path:**
   - In the **Sharing** tab, you will see the network path of the folder, such as `\\YourComputerName\SharedFiles`. Write this down for later use when connecting from your iOS device.

   **Example network path:**
   ```
   \\YourComputerName\SharedFiles
   ```

### Step 2: Connect to the Shared Folder from iOS

With the shared folder set up on her onboard computer, Captain Stellar now turns to her iOS exploration device.

1. **Open the Files app on your iOS device:**
   - This app is pre-installed on iOS devices and is used to access local and network files.

2. **Access the shared folder:**
   - Tap on the **Browse** tab at the bottom of the screen.
   - Tap the three dots (`...`) in the upper-right corner, then tap **Connect to Server**.

3. **Enter the server address:**
   - Type the address of the shared folder in this format: `smb://YourComputerName/SharedFiles`.
   - Tap **Connect**.

4. **Authenticate with your account:**
   - Enter the username and password of the Windows account you shared the folder with.
   - If you used your local Windows account, enter those credentials here.

5. **Access your files:**
   - Once authenticated, the shared folder will appear in the Files app, allowing you to browse, download, and upload files between your iOS device and the Windows PC.

### Step 3: Transfer Files

Now that the devices are securely connected, Captain Stellar begins transferring data between them.

1. **Send files from Windows to iOS:**
   - Simply drag and drop files into the shared folder on your Windows PC. These files will become accessible from the Files app on your iOS device.

2. **Send files from iOS to Windows:**
   - In the Files app on your iOS device, browse to the shared folder and tap the upload icon to add files from your device into the shared folder.

### Tips for Stellar Transfers

- **Security:** For improved security, consider setting up a dedicated user account with limited access and a strong password for file sharing.
- **Connection issues:** Ensure both your Windows PC and iOS device are connected to the same Wi-Fi network.
- **Firewall:** If you have trouble connecting, check that your Windows firewall is not blocking file sharing. You can temporarily disable it or add an exception for "File and Printer Sharing."

With the star maps successfully transferred, Captain Stellar breathes a sigh of relief. Using this secure method, she avoids the risks of third-party networks in deep space and keeps her data safely within her control. Now fully prepared, she heads off to her next mission, knowing her files are secure and easily accessible across the stars.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>