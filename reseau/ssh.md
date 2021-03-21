# SSH

_SSH-key-based authentication_

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

- `ssh-copy-id <login>@<host>`
- `ssh-copy-id -p 1234 u0_a63@192.168.0.17`
- `ssh-copy-id -p 2245 -i ~/.ssh/id_ecdsa.pub u0_a63@192.168.0.14`

> copies `id_ecdsa.pub` on @`<host>` in `~/.ssh/authorized_keys`

If ever ssh-copy-id was not availlable

- `cat ~/.ssh/id_ecdsa.pub | ssh <username>@<remote_host> "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"`

### `ssh-agent`

Helper that keeps track of identity keys and their passphrases

- can use the keys to log into servers without asking the user to type in a password or passphrase again
- mainly used for SSH plublic key authentication

#### `SSH_AGENT_PID`

Checking whether or not `ssh-agent` is running : `echo $SSH_AGENT_PID`

```bash
> echo $SSH_AGENT_PID
1296
```

`SSH_AGENT_PID` is set, since its value is not empty => ssh-agent is more likely running

#### Adding SSH keys to the Agent



## Biblio

- [digitalocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-1604#step-2-%E2%80%94-copy-the-public-key-to-ubuntu-server)
- [ssh.com](https://www.ssh.com/ssh/keygen/)
- [docker alpine](https://wiki.alpinelinux.org/wiki/Setting_up_a_ssh-server)
- [askubuntu_host_key](https://askubuntu.com/questions/87449/how-to-disable-strict-host-key-checking-in-ssh)
