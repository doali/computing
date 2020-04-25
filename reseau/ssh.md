# SSH

## `ssh-keygen`

Tool for creating new authentication key pairs for SSH

- enable automating logins,
- single sign-on,
- authenticating.

### Algorithms

- `rsa` : factoring large numbers

> To avoid...

- `dsa` : computing discrete logarithms

> No longer recommended...

- `ecdsa` : using elliptic curves

> Good (with 521 bits)

- `ed25519` : new !!

> To avoid since new...

```bash
ssh-keygen -t rsa -b 4096
ssh-keygen -t dsa
ssh-keygen -t ecdsa -b 521
ssh-keygen -t ed25519
```

### Generating keys pairs

- `ssh-keygen -t ecdsa -b 521`

### Copying the public key to the server


## Biblio

- [digitalocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-1604#step-2-%E2%80%94-copy-the-public-key-to-ubuntu-server)
- [ssh.com](https://www.ssh.com/ssh/keygen/)
- [docker alpine](https://wiki.alpinelinux.org/wiki/Setting_up_a_ssh-server)
