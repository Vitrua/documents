# Penguin in Outer Space: Basic Linux Workflow

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/linux/penguinspace.jpg?raw=true" alt="Penguin in Space" width="300" height="300">
</div>

## Objective

Learn commands for basic Linux operations from terminal.

## Introduction

Meet Pulsar Penguin, the brave astronaut quietly floating in his spaceship in outer space. As he taps with his fins on the control panel keyboard, his spacecraft is suddenly damaged by a small meteor. Trained to stay calm in such situations, he begins to navigate through the dire scenario.

## Prerequisites

To follow along, you'll need:

- Access to a Linux-based system or terminal emulator.

## Pulsar's Directories

```
engine
├───mounted
│   ├───propeller.broken.part
│   └───jet.part
└───spare
    ├───jet.new.part
    └───propeller.new.part
```

## Linux Commands in Action

### Navigating and Managing Files

- Calmly, Pulsar begins repair operations by determining his current location with the 'print working directory' command:
  ```bash
  pwd
  ```

- Discovering he's in the /engine directory, he confirms its contents with the 'list' command:
  ```bash
  ls
  ```

- Hearing strange noises from the 'mounted' directory, he investigates further using the 'change directory' command:
  ```bash
  cd mounted
  ```

- He finds a broken file, 'propeller.broken.part', and swiftly creates a new directory using 'make directory' to store parts temporarily:
  ```bash
  mkdir temporary
  ```

- Returning to the 'engine' level:
  ```bash
  cd ..
  ```

- He easily makes a 'copy' of the spare part:
  ```bash
  cp spare/propeller.new.part mounted/propeller.new.part
  ```

- Revisiting the 'mounted' components, he renames the new part while 'moving' it:
  ```bash
  mv propeller.new.part propeller.part
  ```

- After completing the repairs, he cleans up the debris by 'removing' unnecessary files:
  ```bash
  rm propeller.broken.part
  rm -r temporary
  ```

### System Management

- Facing a moment of panic when the new part doesn't work due to incorrect permissions, Pulsar temporarily grants full access using the 'change mode' command:
  ```bash
  chmod -R 777 /engine/mounted
  ```

- Encountering an error, he elevates his privileges using the 'super user do' command:
  ```bash
  sudo chmod -R 777 /engine/mounted
  ```

### Communication and Troubleshooting

- With the spaceship stabilized, Pulsar performs a final check to ensure all parts are accounted for using 'global regular expression print':
  ```bash
  grep part
  ```

- Before resuming his journey, he consults the manual one last time:
  ```bash
  man pwd
  ```

## Linux Survival Summary:

- `pwd`: Get the path to the current working directory.
- `ls`: List directory contents. `ls -lah` for more information.
- `cd <directory_name>`: Change directory. `cd ..` to go back to a higher level.
- `mkdir <directory_name>`: Create a new directory.
- `cp <path_original_file> <path_destination_file>`: Copy a file.
- `mv <path_original_file> <path_destination_file>`: Move a file.
- `rm <file_path>`: Remove a file. `rm -rf <directory_path>`: Remove a directory and everything inside it forcefully.
- `chmod <permissions> <file_name>`: Manage permissions.
- `sudo <command>`: Execute a command as a superuser (root).
- `grep <pattern> <file_name>`: Search for a pattern in files.

## Conclusion

Pulsar's journey demonstrates how mastering basic Linux commands can be crucial in critical situations. By familiarizing yourself with these commands, you too can navigate through the complexities of Linux systems with confidence and resilience.


<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>