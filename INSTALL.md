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

## Editing files

Install Atom: https://atom.io

Open it, and then go to Preferences. Click on Install, and search for the package remote-ftp. Install it.

Under the Packages menu, click on Remote FTP, and click on Toogle.

In the new sidebar, click "Edit configuration", and on the blank file that appears on the right (".ftpconfig"), paste the following text:
```bash
{
    "protocol": "sftp",
    "host": "127.0.0.1", // string - Hostname or IP address of the server. Default: 'localhost'
    "port": 3022, // integer - Port number of the server. Default: 22
    "user": "username-of-virtualmachine", // string - Username for authentication. Default: (none)
    "pass": "password-of-virtualmachine", // string - Password for password-based user authentication. Default: (none)
    "promptForPass": false, // boolean - Set to true for enable password/passphrase dialog. This will prevent from using cleartext password/passphrase in this config. Default: false
    "remote": "/home/username-of-virtualmachine/pokecrystal", // try to use absolute paths starting with /
    "agent": "", // string - Path to ssh-agent's UNIX socket for ssh-agent-based user authentication. Linux/Mac users can set "env" as a value to use env SSH_AUTH_SOCK variable. Windows users: set to 'pageant' for authenticating with Pageant or (actual) path to a cygwin "UNIX socket." Default: (none)
    "privatekey": "", // string - Absolute path to the private key file (in OpenSSH format). Default: (none)
    "passphrase": "", // string - For an encrypted private key, this is the passphrase used to decrypt it. Default: (none)
    "hosthash": "", // string - 'md5' or 'sha1'. The host's key is hashed using this method and passed to the hostVerifier function. Default: (none)
    "ignorehost": true,
    "connTimeout": 10000, // integer - How long (in milliseconds) to wait for the SSH handshake to complete. Default: 10000
    "keepalive": 10000, // integer - How often (in milliseconds) to send SSH-level keepalive packets to the server (in a similar way as OpenSSH's ServerAliveInterval config option). Set to 0 to disable. Default: 10000
    "keyboardInteractive": false, // boolean - Set to true for enable verifyCode dialog. Keyboard interaction authentication mechanism. For example using Google Authentication (Multi factor)
    "keyboardInteractiveForPass": false, // boolean - Set to true for enable keyboard interaction and use pass options for password. No open dialog.
    "watch":[ // array - Paths to files, directories, or glob patterns that are watched and when edited outside of the atom editor are uploaded. Default : []
        "./dist/stylesheets/main.css", // reference from the root of the project.
        "./dist/stylesheets/",
        "./dist/stylesheets/*.css"
    ],
    "watchTimeout":500, // integer - The duration ( in milliseconds ) from when the file was last changed for the upload to begin.
    "filePermissions":"0644" // string - Permissions for uploaded files. WARNING: if this option is set, previously set permissions on the remote are overwritten!
}
```

Replace username-of-virtualmachine and password-of-virtualmachine with their respective counterparts.

Click on Connect.

The sidebar will show the files inside the virtual machine.
