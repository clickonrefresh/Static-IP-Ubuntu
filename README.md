# Static-IP-Ubuntu
How to configure a static IP in Ubuntu CL

### Setting a static IP in Ubuntu Server 20.04 LTS

Navigate to the network config file in /etc/netplan, then list the files in that folder.

```text
cd /etc/netplan
ll
```

Your output should look something like this:

![image](https://user-images.githubusercontent.com/72121107/112372389-66354300-8ce8-11eb-801e-788bbe6fdc89.png)

Create a backup of the default file, replace '00-installer-config.yaml with your filename.

```text
cp /etc/netplan/00-installer-config.yaml /etc/netplan/00-installer-config.yaml.bak
```

Now edit the default file to resemble the following configuration, adjusting the addresses to your IP's used.

```text
sudo nano /etc/netplan/00-installer-config.yaml
```

```text
# This is the network config written by 'subiquity', manually ammended for static IP.
network:
  version: 2
  ethernets:
    eth0:
      addresses: [192.168.1.34/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [1.1.1.1, 1.0.0.1]
```

![image](https://user-images.githubusercontent.com/72121107/112372485-87962f00-8ce8-11eb-8846-7abb66d28f21.png)


Save the file and exit.

Try the configuration to see if works

```text
sudo netplan try
```

If successful you will be asked if you want to keep the settings.

Now apply the change and reboot.

```text
sudo netplan apply
sudo init 6
```
