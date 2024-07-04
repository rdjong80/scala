## Install XLArig on a Linux server.

First things first, as a prerequisite you should have installed a linux distribution ( eg. Ubuntu , Debian ) , whether this is on your own hardware or a VPS doesn't matter. 
Instructions on how to install / deploy Linux as a VPS should be provided by the VPS supplier 

You should have posession of a root account on this server, aswell as ssh access to the terminal 
This tutorial is based on a debian 12 linux installation 

You can find installation instructions for debian here:   ( in case of installation on your own hardware ) 

https://www.debian.org/releases/bookworm/installmanual 

Once logged in on the terminal of the linux server we need to take the following steps.
Create a folder were we install xmrig,  normally the /opt folder is were you put software, but this can be any folder ( for example your home dir  ( 
/home/user )  
```bash
 mkdir /opt/xlarig 

 cd /opt/xlarig 
```
Download the latest release of xlarig from github 
```bash
wget https://github.com/scala-network/XLArig/releases/download/v5.2.4/xlarig-v5.2.4-linux-x86_64.zip 
```
Since the xlarig is a zip file, we need to install unzip ( if not present )   
```bash
 apt install unzip 
```
 Then we can unzip the application 
```bash
 unzip xlarig-v5.2.4-linux-x86_64.zip 
```
Next, you can put the command in a bash file ( similar to a windows .bat or .cmd file )  
```bash
 nano mine.sh      (nano is a text editor in linux )
```
The editor opens and now you can put the folowing in the script 

`/opt/xlarig/xlarig -o POOL_ADDRESS -u YOUR_WALLET_ADDRESS_HERE -p WORKER_NAME -a panthera –k `

For settings regarding pool address / url , ports, difficulty settings you should refer to the pool website's FAQ.

To start mining simply type ( in the /opt/xlarig folder)    
```bash
sh mine.sh 
```
Be aware this now runs in the foreground, so when you hit CTRL-C it will stop. To start in background use following command 
```bash
sh mine.sh .& 
```
Alternatively you can configure this to start whenever you reboot by editing the crontab file  

```bash
crontab -e
```

paste the following in the crontab file
 
`@reboot /opt/xlarig/xlarig -o POOL_ADDRESS -u YOUR_WALLET_ADDRESS_HERE -p WORKER_NAME -a panthera –k `

you can add the -t switch at the end to define the number of threads (cpu) you want to work with

## Ubuntu 

For installing on Ubuntu server OS, the steps and prerequisites are basically the same, however on a clean install of ubuntu ( server 22.04 LTS ) i ran into some issues before i could run XLArig.

You may need to install the following packages on Ubuntu before you can use xlarig.

-libssl
-libhwloc

```bash
wget http://nz2.archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.22_amd64.deb

sudo dpkg -i libssl1.1_1.1.1f-1ubuntu2.22_amd64.deb 

sudo apt-get install -y libhwloc-dev 
```


## Windows 

So here's how to setup mining with xlarig on a windows computer, most important is that we need to exclude the xlarig program from scanning by windows Defender ( or any other anti-virus )

in this step-by-step instruction i will user powershell for convenience. It's simple copy and paste the commands.

Search for windows powershell or windows terminal and open it

![image](https://github.com/rdjong80/scala/assets/47658871/902cf9ef-cb70-4e97-bf43-56409fb69d06)

![image](https://github.com/rdjong80/scala/assets/47658871/50a91626-69ec-47ff-999d-dbd7f978aedb)

First disable realtime scanning for windows defender, otherwise we cannot even download the program
```powershell
Set-MpPreference -DisableRealtimeMonitoring $true
```

Next, determine a location on your computer where to store the xlarig program, eg. c:\xla 

create a directory through powershell and download the xlarig application 
```powershell 
mkdir c:\xla

wget https://github.com/scala-network/XLArig/releases/download/v5.2.4/xlarig-v5.2.4-win64.zip

Expand-Archive .\xlarig-v5.2.4-win64.zip
```
add exclusion in windows defender for the c:\xla folder

```powershell
set-mppreference -exclusionpath c:\xla
```
 
next, enable windows defender again.

```powershell
Set-MpPreference -DisableRealtimeMonitoring $false
```



