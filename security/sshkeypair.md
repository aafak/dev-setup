# Passwordless authentication, using public private key pair

**Key Generation:**
**On the client:** You generate a key pair using ssh-keygen. This creates two files:

Private key (id_rsa by default) — this file stays securely on the client machine.
Public key (id_rsa.pub by default) — this file is shared with the servers, after that this client can be authenticated by any servers having this public key

```
aafak@client-machine:~$ ssh-keygen -t rsa -b 2048
Generating public/private rsa key pair.
Enter file in which to save the key (/home/aafak/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/aafak/.ssh/id_rsa
Your public key has been saved in /home/aafak/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:PYQgEHFSBwgJeounQTiQBVxnqXg7VKnBkO8990ev2+s aafak@client-machine
The key's randomart image is:
+---[RSA 2048]----+
|BB@B=+=          |
|*o.=o* . .       |
|+.+ =   . .      |
|.= B     o       |
|o * o   S o      |
| + + o .   o     |
|.   . o . . .    |
|         . ...   |
|          .o+E.  |
+----[SHA256]-----+
aafak@client-machine:~$cat /home/aafak/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQChDpzopPGUYkwrYG...... aafak@client-machine
```

**On the server:**
The server needs to have the public key from the client in its authorized_keys file. This is where SSH checks for authorized keys to authenticate users.

Setting Up the Key-based Authentication
Copy the public key to the server:
aafak@server-machine:~$ vim .ssh/authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQChDpzopPGUYkwrYG...... aafak@client-machine

**Check the server logs for any issue for shh**
```
root@server-machine:/var/log# tail -f auth.log
Nov 22 13:07:36 server-machine sshd[2468544]: Accepted publickey for aafak from CLientIP port 49374 ssh2: RSA SHA256:yUyHlrAAdapLoqRTi6YgdTSsSzLsP0YHlLO/swXP/t0
Nov 22 13:07:36 server-machine sshd[2468544]: pam_unix(sshd:session): session opened for user aafak by (uid=0)
Nov 22 13:07:36 server-machine systemd-logind[768]: New session 2802 of user aafak.

```

**If require Correct permissions on the server:**
Make sure the ~/.ssh directory and authorized_keys file on the server have the correct permissions:
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

**From the client machine try ssh using key:**
aafak@client-machine:~$ ssh -v aafak@serverIP


**How SSH Authentication Works:**
**Client:** The client uses the private key (id_rsa) to create a cryptographic signature during the SSH handshake.
**Server:** The server uses the public key (id_rsa.pub) to verify that the signature matches. If it does, the server grants access.

**Can Any Client Connect Without Password?:**
No, only clients that have the correct private key matching the server's public key can authenticate.
If someone doesn’t have the private key, they cannot connect to the server, even if they know the IP address or username. The private key is essential for authentication.
Even if an attacker has the server’s IP and username, without the private key or the correct passphrase (if set), they cannot authenticate.
Compromised Security Scenarios
Compromised Private Key: If an attacker gets access to the private key (and if it's not protected by a passphrase), they can authenticate as the user. This is why it's critical to protect private keys properly.
Weak or Default Keys: Using weak keys (e.g., short RSA keys) or not regularly rotating keys can make it easier for attackers to brute-force or guess the private key.
Man-in-the-middle Attack: If the client or server is compromised (e.g., through malware or an insecure network), the SSH keys could potentially be intercepted or stolen.
Summary
SSH key-based authentication is secure if used properly, especially when:

The private key is kept secure, ideally protected with a passphrase.
Password authentication is disabled on the server.
Only trusted clients' public keys are added to the authorized_keys file.
Regular monitoring, auditing, and key rotation practices are followed.
So, no, an attacker cannot simply connect to your server without the private key and, if necessary, the passphrase. With proper security measures, SSH key-based authentication is very secure and more resilient to brute-force attacks than password-based authentication.

**Troubleshooting:**

root@server-machine:~# vim  /etc/ssh/sshd_config
PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
MaxSessions 100
root@aafak-virtual-machine:~# sudo systemctl restart sshd


root@server-machine:/var/log# sudo vim  /etc/securetty
tty1
tty2
tty3
tty4

~$ ssh-keyscan -H 172.1.29.165 >> ~/.ssh/known_hosts
# 172.1.29.165:22 SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.3
# 172.1.29.165:22 SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.3
# 172.1.29.165:22 SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.3
# 172.1.29.165:22 SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.3
# 172.1.29.165:22 SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.3

If the client cannot authenticate using the public/private key pair, ensure that:
The client’s public key is properly added to the server’s authorized_keys file.
The permissions on the .ssh directory and the authorized_keys file are correct.
The SSH server configuration allows public key authentication (make sure PubkeyAuthentication yes is set in /etc/ssh/sshd_config).
