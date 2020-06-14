# SSH Configuration

---------

[TOC]

---------

## Generating SSH keys
```shell
# Comment can be Email-PCName
$ ssh-keygen [-t dsa | ecdsa | ed25519] [-b bits] [-C comment]
# Save public/private key as customized name, such as
# /path/to/.ssh/id_dsa_ServiceA and /path/to/.ssh/id_dsa_ServiceA.pub
```

## Set local config file
```shell
# cat ~/.ssh/config
Host HostAlias
    HostName                        DomainName/IP
    User                            UserName
    PreferredAuthentications        publickey
    IdentityFile                    /path/to/.ssh/id_dsa_ServiceA
```

## Add SSH key to the ssh-agent
ssh-agent help us manage private keys and choose the corresponding private
key to authenticate identity without inputing password for private key
```shell
# Ensure ssh-agent is runing
$ eval $(ssh-agent -s)
$ ssh-add /path/to/.ssh/id_dsa_ServiceA
```

## Appplication
### Git
Just copy public_key, go Settings->SSH and GPG Keys->New SSH key to
paste there
```shell
# Test
$ ssh -T git@HostAlias
Some replay from git service...
```

### Server
```shell
# public_key is ~/.ssh/id_dsa_ServiceA.pub
$ ssh-copy-id [-i [public_key]] [user@]hostname
# Test
$ ssh HostAlias
Log in a new shell
```
