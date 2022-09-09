## Environment setup: Windows

### TLDR
1. Install Ubuntu WSL2
2. `sudo apt install netcat curl python3`
3. `python -m ensurepip --upgrade`
4. `python -m pip install pycryptodome pwntools`
5. Install Docker for windows and enable the wsl2 backend
6. Install vscode and enable the `Remote: WSL` extension


### Step 1: Install WSL

Microsoft provides very in depth installation instructions on [https://docs.microsoft.com/en-us/windows/wsl/install](https://docs.microsoft.com/en-us/windows/wsl/install). `Ubuntu` is the OS you want if you have no prior experience with Linux

There's additional steps for setting up your installation at [https://docs.microsoft.com/en-us/windows/wsl/setup/environment](https://docs.microsoft.com/en-us/windows/wsl/setup/environment)
- This includes information on setting up `docker` and `vscode`, both of which you should install in a bit
- Optional: WSL can be a bit sluggish with it's default settings, check out [https://jade.fyi/blog/development-in-wsl/](https://jade.fyi/blog/development-in-wsl/) for some more tuning

### Step 2: Install basic tools

`apt` is the package manager for Ubuntu, and it's what you'll use to install and update software for your WSL installation

Run `sudo apt install netcat curl python3` in the terminal to install basic tools

In the future, run `sudo apt update` and `sudo apt upgrade` occasionally to keep everything up to date

### Step 3: Install python libraries

`pip` is the package manager for Python and you'll use it to install libraries and keep them up to date

`virtualenv` creates small environments that you can safely install your tools into without having to worry about it affecting the rest of your system

Run `mkdir ctf` to make a folder to put all your ctf related stuff in and `cd ctf` to move into it

Run `python3 -m venv ctf` to create a virtual environment (this may take awhile) and run `source ctf/bin/activate` to activate it. You should now see a little `(ctf)` on your terminal prompt

Run `python -m ensurepip --upgrade` to install `pip`

Run `python -m pip install pycryptodome pwntools` to install the two libraries you'll need (this may take awhile)

Run `deactivate` after you're done to leave the virtual environment. Remember to run `source ctf/bin/activate` each time you restart your terminal to enter the venv

### Step 4: Install docker and vscode

Visual studio code is a versatile editor with great integration with WSL, I recommend it if you don't have a particular preference for editor [https://code.visualstudio.com/](https://code.visualstudio.com/)

Instructions for installing Docker with the WSL2 backend can be found on [https://docs.docker.com/desktop/windows/wsl/](https://docs.docker.com/desktop/windows/wsl/) 

Details for enabling the WSL features
- [https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode)
- [https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-containers](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-containers)