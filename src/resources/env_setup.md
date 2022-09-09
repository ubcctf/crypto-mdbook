## Environment setup

For solving CTF challenges in general, there's a few things that you'll need. Specific instructions for how to install these tools are in their respective OS pages
- [Windows](./env/windows.md)
- [Mac](./env/mac.md)

### A Linux shell

While not a strict requirement technically, a linux shell will almost inevetiably become a requirement as you do more CTF challenges. Installing tools, running binaries, debugging, these are all much easier to do with a fully fledged linux shell vs using a shell emulator or something like powershell

The good part is that installing a proper linux environment is now quite easy
- MacOS comes with one pre-installed
- Windows now supports Windows Subsystem for Linux (WSL) v2, which is easy to install and gives you everything you need

### Basic tools

A basic suite of tools you'll want are
- `python`, the programming language of choice for most CTFers. Comes preinstalled on all linux shells
   - You'll want some additional libraries though, namely `pycryptodome` which implements all the cryptographic algorithms you'll need, and `pwntools` which makes connecting to servers programatically easy
- `netcat`, a tool for connecting to ports on servers, which is what you'll need to do to connect to challenge instances
- `curl`, a tool for making http/https requests, useful for challenges that are on websites

### Docker

Docker is a tool that lets you package up a "mini vm" of sorts as a list of instructions. This lets challenge authors give you a `Dockerfile` and let you rebuild the challenge server for your own local testing, which you'll definitely want to be able to do