---
title: SSH keys
teaching: 5
exercises: 0
objectives:
- "Understand what SSH keys can be used for"
- "Setting up a secure SSH key for personal use"
- "Copying the key to the PPI system"
---
# Introduction to SSH keys

1. [Generally about keys](#generally-about-keys)
2. [SSH keys](#ssh-keys)
3. [Copying the key to VGL](#copying-the-key-to-vgl)
4. [Important files](#important-files)

## Generally about keys

A key pair consisting of a private and a public key can be used for authentication, signing/verification, or encryption/decryption. The underlying principle is that:
- what is encrypted with the public key can only be decrypted with the corresponding private key, and vice versa;
- what is encrypted with the private key can only be decrypted with the corresponding public key.

Both SSH, GPG, and CA keys are key pairs consisting of a private and a public key.

Keys can be generated with different algorithms and lengths, affecting the degree to which an attacker might gain access through brute force code cracking. 
Additionally, some types of keys can be created with expiration dates to prevent potential harm if their management fails. 
The use of shared keys versus personal keys can result in a loss of traceability and an increased likelihood of keys being compromised, especially when someone leaves, among other challenges.

## SSH Keys

SSH keys are used at MET to authenticate a person or machine to:
- Read or modify information on a Git service like gitlab.met.no, git.ik.met.no, or github.com
- Execute commands with limited or extended privileges on a virtual or physical machine

In this course we are concerned with personal keys. 

### Creating a New SSH Key

The recommended method is:

```bash
ssh-keygen -t rsa -b 4096 -a 250 -C "$USER@$(hostname) $(date)"
```

Choose a strong password for the private key!
For added security it is possible to store the key on a physical, secure key, though we will not cover that in this course.

## Copying the key to VGL

To copy a key to PPI, use the following command:

```bash
ssh-copy-id $USER@ppi-r8login-a1.int.met.no
```

This command is used to copy your SSH public key to the authorized_keys file on the specified PPI server, allowing you to authenticate without entering a password. 
Make sure to replace $USER with your actual username.


## Important files

Your ~/.ssh catalog has your key pair. 

- id_rsa is your private key. *Keep it secret, keep it safe!*
- id_rsa.pub is your public key 

On a server,

- authorized_keys has a copy of your public key


> Excercise: Can you find out how many SSH keys you have at the PPI system?
>
>> Solution: 
>>~~~
>>ssh ppi-r8login-a1.int.met.no
>>cat .ssh/authorized_keys | wc -l
>>~~~

> Excercise: If you have more SSH keys than you need, shall we clean the excess ones out?
>
>> Solution:                               
>>Log in on the PPI system and remove unnecessary files from the ~/.ssh/authorized_keys file. 
>>We have worked a lot with things like this today!

---

[Previous slide](README.md)
[Next slide](02-End.md)
