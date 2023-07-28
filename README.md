# Windows Setup

Step-by-step guide for making a Windows machine bearable and usable (i.e. macOS/Linux-like).

> The instructions in this repository have been tested with **Windows 10**.

## Introduction

If you're reading this, you're probably a non-Windows user who is forced, through whatever circumstances, to work on a Windows machine (_ugh!_). This repository contains instructions to get out of the hell as quick as possible and create an environment that resembles macOS/Linux as much as possible.

The survival guide consists mainly of the following parts:

1. Configure Windows settings
1. Install Linux with [WSL 2](https://learn.microsoft.com/en-us/windows/wsl/)

Let's bite the bullet and go through it!

## Configure Windows settings

> The following instructions are sorted by urgency, that is, the most insufferable things are fixed first and the more tolerable things are addressed later. So, it's best to follow the guide in this order.

### 1. Install a custom keyboard layout

> This step is optional if you're not content with any of the included keyboard layouts of Windows.

To install a custom keyboard layout, follow the instructions [👉 here](https://github.com/weibeld/logitech-swiss-german-keyboard-layout#windows).

The above instructions are for an example keyboard layout (Logitech Swiss German), however, it works the same for any keyboard layout. All you need for it is your desired keyboard layout as a `.klc` file.

### 2. Install custom key remappings

To install a set of custom key remappings, follow the instructions [👉 here](https://github.com/weibeld/autohotkey-windows-key-remappings).

The remappings in the above instructions make the Windows keyboard more similar to a macOS keyboard (for example, use _Win-C_ instead of _Ctrl-C_ for copying, thus resembling _Cmd-C_ on macOS). They also swap the _Caps Lock_ and _Ctrl_ keys, a common customisation among macOS/Linux users to make the _Ctrl_ easier to press.

> Note: the key remappings are independent of the used keyboard layout.

### 3. Customise the touchpad

In _**Settings > Devices > Touchpad > Taps**_, make the following changes:

1. Set _**Touchpad sensitivity**_ to _**Low sensitivity**_
1. Unselect _**Press the lower right corner of the touchpad to right-click**_
1. Unselect _**Tap twice and drag to multi-select**_

### 4. Customise the taskbar

1. In _**Settings > Personalization > Taskbar**_, make the following changes:
   1. Select _**Combine taskbar buttons > Always hide labels**_
   1. Disable _**News and interests > Show news and interests on the taskbar**_
   1. Enable _**Notification area > Select which icons appear on the taskbar > Always show all icons in the notification area**_
   1. Disable all items except _**Clock**_, _**Volume**_, _**Network**_, and _**Power**_ from _**Notification area > Turn system icons on or off**_
1. In _**Settings > Personalization > Start**_, make the following changes:
   1. Disable all items except _**Show app list in Start menu**_
1. Right-click on taskbar and make the following changes:
   1. Enable _**Search > Show search icon**_

### 5. Miscellaneous settings

1. Disable the [Task View](https://en.wikipedia.org/wiki/Task_View) timeline:
   1. In _**Settings > Privacy > Activity history**_, unselect everything
   1. In _**Settings > System > Multitasking**_, disable _**Timeline**_
1. Disable automatic display brightness adjustment:
   1. In _**Settings > System > Display**_, disable _**Change brightness automatically when lighting changes**_
1. Disable the system beep ("bell") sound:
   1. In _**Settings > System > Sound > Related Settings > Sound Control Panel > Sounds**_, set _**Default Beep > Sounds**_ to _**None**_

### 6. Install and configure Windows Terminal

[Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/) is Microsoft's replacement for the old _Windows Console_ that has been traditionally used for running shells like _Command Prompt_ and _PowerShell_. Windows Terminal can run any number of shells (including _Command Prompt_ and _PowerShell_) organised in profiles.

Since Windows Terminal is relatively new (introduced in 2019, see [announcement](https://devblogs.microsoft.com/commandline/introducing-windows-terminal/)), it is not yet included in Windows by default and must be manually installed.

**After installing Windows Terminal, you can forget about the existence of the built-in _Command Prompt_ and _PowerShell_ applications, you will never need to use them again!**

#### Installation

There are two ways to install Windows Terminal:

- With `winget`:
  ```powershell
  winget install Microsoft.WindowsTerminal
  ```
- From GitHub:
  1. Locate the desired version on https://github.com/microsoft/terminal/releases
  1. Download the `.msixbundle` file from the GitHub release and install it by double-clicking

> You might not get the newest version of Windows Terminal with `winget`, thus, if you want the newest version, install from GitHub.

After installation, open Windows Terminal by typing `wt` into the Windows search box.

#### Configuration

To configure Windows Terminal, apply the custom settings from [👉 here](https://github.com/weibeld/windows-terminal-settings):

1. In Windows Terminal, press _**Shift-Ctrl-Comma**_ to open the settings file
1. Overwrite the content of the settings file with the custom settings in [`settings.json`](https://github.com/weibeld/windows-terminal-settings/blob/main/settings.json)
1. Save the Windows Terminal settings file and restart Windows Terminal

> As mentioned, Windows Terminal is the only terminal application that you will ever need from now on. WSL 2 will run from Windows Terminal, and if you need _Command Prompt_ or _PowerShell_ you can run them in Windows Terminal too (through their corresponding profiles).

### 7. Install Git for Windows

This is not for using Git on Windows (_God forbid!_) but for making the [Git Credential Manager](https://github.com/git-ecosystem/git-credential-manager) available to the Linux distributions in WSL 2 (that will be installed later). This is the [recommended way](https://github.com/weibeld/windows-terminal-settings/blob/main/settings.json) of setting up Git credentials in WSL 2.

Install Git for Windows as follows:

1. Locate the latest stable release on https://github.com/git-for-windows/git/releases
1. Download the `*-64-bit.exe` file
1. Install by double-clicking the `.exe` file and accepting all the default options

### 8. Set up eduroam

> This step is optional and applies only if you have [eduroam](https://eduroam.org/) access (linked repo below is private).

Set up access to eduroam by following the instructions [👉 here](https://github.com/weibeld/eduroam-setup).

## Install Linux with WSL 2

Now that Windows itself is a tiny bit less insufferable, it's time to install Linux on it so that you can forget about 90% of the time that you're actually working on Windows.

One possible way to do this is with the [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/) version 2.

> Alternative ways are running Linux in a virtual machine (VM) or setting up Windows/Linux [dual boot](https://en.wikipedia.org/wiki/Multi-booting).

Note that the following instructions will use Ubuntu as an example Linux distributions, however, the process remains largely the same for other Linux distributions.

### 1. Enable WSL 2

WSL 2 is included by default in Windows and it just needs to be enabled. This can be done as follows:

1. Type `wt` in the Windows search bar and click on _**Run as administrator**_
1. In the _Command Prompt_ or _PowerShell_ that opens, execute:
   ```powershell
   wsl --install
   ```
1. Exit Windows Terminal

### 2. Installing a Linux distribution

With WSL 2 enabled, it's possible to install a Linux distribution.

From _Command Prompt_ or _PowerShell_ in Windows Terminal, run the following to list all the Linux distributions that are available for installation:

```powershell
wsl -l -o
```

To install the _Ubuntu_ distribution, run:

```powershell
wsl --install Ubuntu
```

The above might take a while and you are also prompted to set a username and password for the Linux user. Note that this is completely independen from your user account on Windows.

Once the installation is comlete, you can list all installed Linux distributions with:

```powershell
wsl -l -v
```

To start the _Ubuntu_ distribution, execute the following:

```powershell
wsl -d Ubuntu
````

This drops you into the Ubuntu command line within Windows Terminal.

### 3. Creating a Windows Terminal profile

Since 99% of the time when you open a terminal you want to use your WSL 2 Linux distribution, it's best to create a corresponding Windows Terminal profile and set it as the default profile. In this way, whenever you open Windows Terminal, you're dropped straight into your Linux distribution.

To do so, proceed as follows:

1. In Windows Terminal click _Ctrl-Comma_ to open the settings
1. In the left settings pane, click on _**Add a new profile > New empty profile**_ and configure the following parameters:
   1. _**Name:**_ any name representing the Linux distribution (e.g. `WSL2 Ubuntu`)
   1. _**Command line:**_ `wsl -d Ubuntu`
   1. _**Icon**_: any image file representing the Linux distriubtion (check [👉 here](https://github.com/weibeld/windows-terminal-settings/tree/main/icons))
1. In the left settings pane, go to _**Startup**_ and set _**Default profile**_ to the profile you just created
1. Click _**Save**_ in the lower right corner

After that, quit and restart Windows Terminal and you should be dropped right into your Linux distribution.

> It's possible that Windows Terminal has already auto-created a profile for the detected WSL 2 Linux distributions. Of course, you can also use this auto-created profile, or else you can safely delete it.

### 4. Setting up Linux

TODO: create Linux setup script on GitHub and apply it here.