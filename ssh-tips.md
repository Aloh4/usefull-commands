**ssh quiet output**
```
ssh -q
```

**Remove pergunta (yes/no) e não salva hash em known_hosts**
```
ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null username@password
```


**SSH com algoritmos/cifras legadas via comando:**
```
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 -c aes128-cbc username@password
```

**Inserir algoritmos/cifras no /etc/ssh/ssh_config:**

```
#Legacy changes
#Mais conhecidos, inserir conforme necessidade e não todos
KexAlgorithms diffie-hellman-group1-sha1,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1
Ciphers 3des-cbc,blowfish-cbc,aes128-cbc,aes128-ctr,aes256-ctr

# Após inserir, reiniciar processo SSH
```

**Lendo saída ssh -v**
* ssh -V outputs to `STDERR`, not `STDOUT`
```
ssh_version=$(ssh -V 2>&1)
grep -o "OpenSSH_7.4p1" <<< "$ssh_version"

or..

ssh -V 2> file.txt
ssh -V > /tmp/ssh_version_check.txt 2>&1
```
