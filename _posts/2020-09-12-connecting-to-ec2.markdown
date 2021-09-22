---
layout: post
title:  "Connecting to EC2"
date:   2020-09-12 19:03:04 +1200
---

During EC2 launch download private key. It is a file with `.pem` extension.

To connect to EC2 instance using the key on Windows:
- Use PowerShell version 7
- And run command:
```
ssh ec2-user@1.1.1.1 -i '.\file.pem'
```

If this is the first connection to the server the following question is asked:
```
The authenticity of host '1.1.1.1 (1.1.1.1)' can't be established.
ECDSA key fingerprint is SHA256:tT1Nnbxz7GsfsfwfsfqiTzdfgdgdZ4IOdfvof/s4g.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```
There could be a security risk with connecting to a machine. If the machine has been spoofed by a malicious actor the credentials (such as private key) can be intercepted by attacker.
If this is a connection to a new machine created just minutes ago it is perfectly fine to accept the risk and type `yes`. In response we get:

```
Warning: Permanently added '54.91.16.103' (ECDSA) to the list of known hosts.
```

Next obstacle can look like this:
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions for '.\file.pem' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key ".\file.pem": bad permissions
ec2-user@1.1.1.1: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
```
To overcome this:
- Open file properties
- Go to Security tab
- Click `Advanced`
- Click `Disable inheritance`
- Add your identity (the account used to log in to Windows)
- Add `Full Control` to yourself
- Remove other principals

Next time we run:

```
ssh ec2-user@1.1.1.1 -i '.\file.pem'
```
we should be able to see:
```

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
[ec2-user@ip-172-31-29-209 ~]$
```


