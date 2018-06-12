# Instructions

These are instructions to build the pokecrystal dissasembly inside a virtual machine, so the installation doesn't change our main operative system.

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
ssh -p 3022 username-of-virtualmachine@127.0.0.1
```

Replace username-of-virtualmachine with the actual username.

Answer "yes" when the warning appears.

Write the virtual machine's password, and you'll be in.

## Installing dependencies

Write the following commands:

```bash
sudo apt-get install make gcc bison git flex pkg-config libpng-dev virtualbox-guest-x11
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

## Accesing the files

In the terminal, type the next command to turn the virtual machine off:

```bash
sudo shutdown now
```

Create a folder, called pokecrystal, in your Host system.

Now go to the main Virtual Box window, and select your virtual machine, and click in Settings. Click Shared folders.

Click the "plus" button. In the new window, in "Folder path", click the arrow and select "other". Navigate to the pokecrystal folder created in the host system, and inside the folder, click "Open". In "Folder name", leave "pokecrystal". Check Auto-mount, and then click Ok in all the windows. This will create a shared folder between the host and the guest.

Select the virtual machine and click on Start->Headless start again.

Open the terminal again, and login to the virtual machine, with the command:

```bash
ssh -p 3022 username-of-virtualmachine@127.0.0.1
```

After you login, we have to make sure that the shared folder was correctly created. Type:

```bash
ls /media/
```

If a folder "sf_pokecrystal" is listed, it was correctly created. If not, check the previous steps.

Now you have to grant access to the user of the virtual machine to this folder:

```bash
sudo usermod -a -G vboxsf username-of-virtualmachine
```

To make effect, you have to restart the virtual machine, so type:

```bash
sudo reboot
```

The virtual machine will disconnect. After a little while, you can login again, so type:

```bash
ssh -p 3022 username-of-virtualmachine@127.0.0.1
```

Now we want to copy all the files from the pokecrystal directory inside our virtual machine, to the shared folder. To do so:

```bash
cp -a pokecrystal/. /media/sf_pokecrystal/
```

You will see all of the files in the pokecrystal folder on your host system.

## Editing the files

Install Atom: https://atom.io

Open it, and go to File->Open. Select the pokecrystal folder recently created, and click in Open. The folder will be displayed in the left panel. You can freely edit the files, and those will be synced with the virtual machine.

## Testing your changes

Everytime you need to test your changes, you need to build the rom inside the sf_pokecrystal of your virtual machine. To do so, the virtual machine must be started ('headless start'), and in the terminal, once you're logged in the virtual machine, type:

```bash
cd /media/sf_pokecrystal
make
```

Now, open the pokecrystal.gbc inside the pokecrystal folder using any GameBoy emulator, like VisualBoyAdvance: https://sourceforge.net/projects/vba/.
