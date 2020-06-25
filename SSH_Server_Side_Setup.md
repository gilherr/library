# SSH Server Setup and Usage

## Setup Server Side

```bash
sudo apt-get install openssh-server net-tools
```

Check to see if server is listening

```bash
$ netstat -tupln

tcp     0.0.0.0:22      0.0.0.0:*       LISTEN
```

Find the server's local ip with `ifconfig` or `hostname -I`.

### Setup Key Based Connection

Edit `/etc/ssh/sshd_config` and change the following lines:

```bash
PermitRootLogin no
PasswordAuthentication no
```

Now restart the service with

```bash
sudo service ssh restart
```

see [Key Generation](#key-generation) for user side steps.

## Connect From User Machine

To rename a server's address, append `<address>   <name>` to the `/etc/hosts` file.

To connect to remote machine:

```bash
ssh <username>@<server-address>
```

### Key Setup

```bash
# Generate Key
$ ssh-keygen -t rsa -b 4096                                                                     255 ↵

# Copy *PUBLIC* key to remote machine
$ scp <keyname>.pub <username>@<address>:/home/<username>/.ssh/uploaded.pub
```

Now on the remote machine

```bash
cat ~/.ssh/uploaded.pub >> authorized_keys
chmod 700 ~/.ssh
chmod 600 ~/.ssh/*
```

Now you can connect using the keys.
Note that you might need to look into the config at `/etc/ssh/sshd_config` if
to change things like root login or allow password connections.
