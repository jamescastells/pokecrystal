# Instructions

## Installing the virtual machine

Download Virtualbox from https://www.virtualbox.org

Download Ubuntu server from https://www.ubuntu.com/download/server

Create a virtual machine and install Ubuntu.

Once installed, login into the virtual machine and run:

```bash
sudo apt-get install openssh-server
```

Once installed, run

```bash
shutdown now
```

## Granting access

In Virtualbox, select the virtual machine and click Settings. In "Network", click "Advanced" and then "Port forwarding".

Click the "+" to create a new rule. Under Host port, write 3022, and on the right, under Guest Port, write 22. Accept all the dialogs.

In the main window, click on the arrow next to "Start" and select "Headless start". The virtual machine will now display "Running".

On your host system, make sure you have SSH installed. Open a terminal and write:

```bash
ssh -p 3022 username-of-ubuntu@127.0.0.1
```

Replace username-of-ubuntu with the actual username.

Answer "yes" when the warning appears.

Write the virtual machine's password, and you'll be in.

## Installing dependencies

Write the following commands:

```bash
sudo apt-get install make gcc bison git flex pkg-config libpng-dev
git clone https://github.com/rednex/rgbds
cd rgbds
sudo make install
cd ..
```

## Installing the source code

```bash
git clone https://github.com/pret/pokecrystal
cd pokecrystal
make
```
