# Linux

## Linux Users Management

### Add New Users

create a new user. note that its different than `useradd`.

```bash
adduser <username>
```

Change [create] user's password

```bash
passwd <username>
```

Check if user was created succesfuly

```bash
cat /etc/passwd | grep <username>
```

### Add User to Group

```bash
#  i.e:        sudo      gil
$ usermod -aG <group> <username>
```

### Delete Users

Use `-r` to remove the user's `Home` folder.

```bash
userdel -r <username>
```

### Change Current User

```bash
su - <username>
su -              # this changes to root user
```

### References

- [tecmint](https://www.tecmint.com/add-users-in-linux/)

## Datetime

### Set System Time

taken from [here](https://www.garron.me/en/linux/set-time-date-timezone-ntp-linux-shell-gnome-command-line.html)

```bash
# set timezone
cp /usr/share/zoneinfo/Israel /etc/localtime

# set system time
date -s "03 MAR 2019 23:33:00"

# set hardware clock
hwclock --set --date="2019-03-03 23:30:00" --localtime

```
