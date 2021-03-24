# Static-IP-Ubuntu
How to configure a static IP in Ubuntu CL


### Navigate to the network config file in /etc/netplan, then list the files in that folder.

```code
cd /etc/netplan
ll
```

#### Your output should look something like this:

![image](https://user-images.githubusercontent.com/72121107/112372389-66354300-8ce8-11eb-801e-788bbe6fdc89.png)


__________________________________________________________________________________________________________________

### Create a backup of the default file, replace '00-installer-config.yaml with your filename.

```
cp /etc/netplan/00-installer-config.yaml /etc/netplan/00-installer-config.yaml.bak
```

_________________________________________________________________________________________________________________

### Now edit the default file to resemble the following configuration, adjusting the addresses to your IP's used.

``` Type 'ip a' to find the name of your network adapter and replace it in 'eth0' ```


```
sudo nano /etc/netplan/00-installer-config.yaml
```

```
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


#### Save the file and exit. "Ctrl+o" , 'enter' , "Ctrl+x"

_________________________________________________________________________________________________________________________________

### Try the configuration to see if works

```
sudo netplan try
```

### If successful you will be asked if you want to keep the settings. Press 'enter' to accept.

#### Now apply the change and reboot.

```
sudo netplan apply
sudo init 6
```
