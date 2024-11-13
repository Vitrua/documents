# Power-Saving 2-HDD Ubuntu Server Setup

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/workflows/2bays.jpg?raw=true" alt="2bays" width="300" height="300">
</div>

## Objective
Learn how to configure an energy-efficient 2-HDD setup on an Ubuntu server using cron jobs, rsync for syncing, and power management tools—all to reduce energy usage while ensuring data security.

---

## The Tale of the Persistent Mariner and the Slumbering Sailor

In the vast ocean of Cloudoria, a ship captain named Captain Net embarked on a quest to manage his storage fleet. The ship’s **Persistent Mariner** (the first disk) worked tirelessly, keeping the ship’s records organized and accessible at all times. But beside it rested a **Slumbering Sailor** (the second disk), who awoke only once a week to synchronize data, aiding the captain in preserving precious cargo without draining the ship’s energy.

To maintain this balance, Captain Net needed a strategy to control the Slumbering Sailor’s awakenings and to allow the Persistent Mariner to conserve energy when idle.

---

## Preparing the Ship’s Log and Storage

### 1. **Identifying the First Mate and Slumbering Sailor**

Captain Net started by identifying each disk’s identifier:

```bash
lsblk
```

In the device list, he found:
- The **Persistent Mariner** (`/dev/sdb`) was mounted at `/mnt/disk1`, always prepared for the crew’s needs.
- The **Slumbering Sailor** (`/dev/sdc`) would only mount at `/mnt/disk2` for the weekly sync.

### 2. **Creating a Dock for the Slumbering Sailor**

To ensure the Slumbering Sailor had a safe place to mount when needed, the captain created a mount point:

```bash
sudo mkdir -p /mnt/disk2
```

### 3. **Writing the Weekly Sync Routine**

Captain Net penned a script, naming it `weekly_sync.sh`, to summon the Slumbering Sailor weekly, sync data with the Persistent Mariner, and let it rest once again. He placed it in the `/usr/local/bin/` directory:

```bash
#!/bin/bash

# Defining paths and devices
DISK1="/mnt/disk1"
DISK2="/mnt/disk2"
DEVICE="/dev/sdc" # Identifier of the Slumbering Sailor

# Step 1: Mount the Slumbering Sailor
sudo mount $DEVICE $DISK2 || { echo "Failed to mount $DEVICE"; exit 1; }

# Step 2: Sync Persistent Mariner's data with the Slumbering Sailor
rsync -av --delete $DISK1/ $DISK2/

# Step 3: Unmount the Slumbering Sailor
sudo umount $DISK2

# Step 4: Power down the Slumbering Sailor
sudo udisksctl power-off -b $DEVICE
```

After finishing, Captain Net made the script executable:

```bash
sudo chmod +x /usr/local/bin/weekly_sync.sh
```

### 4. **Scheduling the Sync Using the Tides of Cron**

Using a `cron` job, Captain Net scheduled his script to wake up the Slumbering Sailor every Sunday at 2:00 AM.

To configure this, he opened the cron editor:

```bash
crontab -e
```

Then, he added the following line to ensure the Slumbering Sailor would reliably appear:

```bash
0 2 * * 0 /usr/local/bin/weekly_sync.sh
```

With this, each week, the Slumbering Sailor would awaken, sync with the Persistent Mariner, and return to sleep, saving energy and maintaining safe data backups.

---

## Bestowing Rest Upon the Persistent Mariner

To help the Persistent Mariner conserve energy during calm seas, Captain Net used `hdparm`, an efficient power-management tool.

### 1. **Installing `hdparm`**

Captain Net ensured `hdparm` was available on his ship’s server:

```bash
sudo apt update
sudo apt install hdparm
```

### 2. **Setting an Idle Timer**

He then set the Persistent Mariner to spin down automatically after 10 minutes of inactivity, reducing energy use without compromising availability.

```bash
sudo hdparm -S 120 /dev/sdb
```

- **`-S 120`**: This value sets the spin-down timer to 10 minutes (120 units of 5 seconds each).

To make this setting persistent across reboots, he added it to the system configuration file:

```bash
echo "/dev/sdb { spindown_time = 120 }" | sudo tee -a /etc/hdparm.conf
```

### 3. **Setting Advanced Power Management (Optional)**

For more energy efficiency, he used **Advanced Power Management**:

```bash
sudo hdparm -B 127 /dev/sdb
```

- **`-B 127`**: This option allows for moderate power savings without impacting the Persistent Mariner’s performance.

---

## Summary of Captain Net’s Routine

1. The Slumbering Sailor powers on weekly to sync with the Persistent Mariner, then returns to rest.
2. The Persistent Mariner spins down automatically after 10 minutes of inactivity, conserving energy.

With this setup, Captain Net’s storage fleet would be energy-efficient and reliable, ready to protect their valuable data for many voyages ahead.

---

### Commands Summary:

- **Sync Script**: Schedule weekly syncing using `rsync` and `udisksctl` to power down the Slumbering Sailor.
- **Cron Job**: Use `crontab -e` to configure the weekly sync.
- **Spin-Down**: `hdparm -S 120 /dev/sdb` — Set a spin-down timer for the Persistent Mariner.
- **Advanced Power Management**: `hdparm -B 127 /dev/sdb` — Moderate power-saving settings.

```markdown
ship-storage-setup/
├── weekly_sync.sh # Automates the syncing process and powers down the Slumbering Sailor
└── hdparm.conf    # Stores persistent power management settings
```

Captain Net’s journey came to a satisfying end, knowing his disks would be loyal, energy-efficient stewards of his server’s data for many voyages ahead.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>
