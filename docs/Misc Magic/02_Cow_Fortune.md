# Cow Fortune

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/misc/cowfortune.jpg?raw=true" alt="misc" width="300" height="300">
</div>

## Storytime
Fortune-teller cow wasn't known for her milk production,

but for her uncanny ability to see the future. 

Farmers flocked to her pasture, eagerly awaiting a swish of her tail 

(left meant sunshine, right meant rain). 

## Objective

Transform your mundane bash terminal into a whimsical oracle of fortunes with the mystical insights of the Fortune-teller Cow. Each time you open your terminal, be greeted by a prophetic message delivered by the wise bovine seer.

## Example

```bash
 ___________________________________
< Beware of low-flying butterflies. >
 -----------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

## Installation

1. **Install fortune and cowsay**
    
    First, you need to ensure that both `fortune` and `cowsay` are installed on your system. You can do this using your package manager. For example, on Ubuntu or Debian-based systems, you can use `apt`:
    
    ```bash
    sudo apt update
    sudo apt install fortune cowsay
    ```
    
    For other Linux distributions, you might use `yum`, `dnf`, or another package manager appropriate to your system.
    
2. **Modify your .bashrc file**
    
    Once you have `fortune` and `cowsay` installed, you can modify your `.bashrc` file to display a random fortune each time you open a new terminal window or tab.
    
    Open your `.bashrc` file in a text editor. You can do this with the following command:
    
    ```bash
    nano ~/.bashrc
    ```
    
    Scroll to the bottom of the file, and add the following lines:
    
    ```bash
    # Display a random fortune with cowsay when opening a new terminal
    if [ -x /usr/games/cowsay -a -x /usr/games/fortune ]; then
      fortune | cowsay
    fi
    ```
    
    Save the file by pressing `Ctrl + O`, then press `Enter` to confirm, and exit Nano by pressing `Ctrl + X`.
    
3. **Test it out**
    
    Open a new terminal window or tab, and you should see a random fortune displayed in a speech bubble created by a cow! Each time you open a new terminal, you'll see a different fortune.
    
That's it! You've successfully installed `fortune` and `cowsay` on your Bash shell and configured it to display a random fortune each time you open a new terminal session.
    
<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>