# ssh-config
[![Build Status](https://travis-ci.org/kkirsche/ssh-config.svg?branch=master)](https://travis-ci.org/kkirsche/ssh-config) [![GoDoc](https://godoc.org/github.com/kkirsche/ssh-config?status.svg)](https://godoc.org/github.com/kkirsche/ssh-config)

A cross-platform sshd configuration file manager allowing for easily adding and removing host configurations.

## Installation

### From Source

```shell
~ ❯❯❯ go get -u github.com/kkirsche/ssh-config
```

### Homebrew

Coming Soon!

<!-- ```shell
~ ❯❯❯ brew update && brew install ssh-config
``` -->

## Examples

### Check SSH Configuration File For File Ownership and Permission Errors

```shell
~ ❯❯❯ ssh-config doctor
[Doctor Action] Opening local SSH configuration at /Users/kkirsche/.ssh/config
[Doctor Success] Global configuration file is correctly owned.
[Doctor Success] Global configuration file is correctly owned.

~ ❯❯❯ ssh-config doctor -v
Using config file: /Users/kkirsche/.ssh/config
[Doctor Action] Opening local SSH configuration at /Users/kkirsche/.ssh/config
[Doctor Success] Global configuration file permissions are -rw-r--r-- (0644)
[Doctor Success] Global configuration file is correctly owned.
[Doctor Action] Opening global configuration at /etc/ssh/ssh_config
[Doctor Success] Global configuration file permissions are -rw-r--r-- (0644)
[Doctor Success] Global configuration file is correctly owned.
```

### Add Entries to Configuration File(s)

```shell
~/Desktop ❯❯❯ touch testConfig
~/Desktop ❯❯❯ ssh-config add -r "1.2.3.4" -p 22 -u "example" -w "/Users/kkirsche/Desktop/testConfig" -v Ghost
Using config file: /Users/kkirsche/.ssh/config
[Add Info] Detected passed arguments: [Ghost]. Combined as: Ghost.
[Add Info] Printing SSH configuration entry to stdout.

Host Ghost
Hostname 1.2.3.4
Port 22
User example

[Add Success] SSH Configuration Entry Successfully Appended
~/Desktop ❯❯❯ cat TestThis
Host Ghost
Hostname 1.2.3.4
Port 22
User example
```

### Show Configuration File(s)

#### Show Current User Configuration File Contents
```shell
~ ❯❯❯ ssh-config show user
# /Users/example/.ssh/config
Host ExampleWebsite
HostName 1.2.3.4
Port 22
User toor
```

#### Show Global Configuration File Contents
```shell
~ ❯❯❯ ssh-config show global
#	$OpenBSD: ssh_config,v 1.26 2010/01/11 01:39:46 dtucker Exp $

# This is the ssh client system-wide configuration file.  See
# ssh_config(5) for more information.  This file provides defaults for
# users, and the values can be changed in per-user configuration files
# or on the command line.

# Configuration data is parsed as follows:
#  1. command line options
#  2. user-specific file
#  3. system-wide file
# Any configuration value is only changed the first time it is set.
# Thus, host-specific definitions should be at the beginning of the
# configuration file, and defaults at the end.

# Site-wide defaults for some commonly used options.  For a comprehensive
# list of available options, their meanings and defaults, please see the
# ssh_config(5) man page.

 Host *
   SendEnv LANG LC_*

# Configuration options and default values (see ssh_config(5) for their meaning):
#
#   Host # (no default)
#   AddressFamily any
#   AskPassGUI yes # (Apple only)
#   BatchMode no
#   BindAddress # (no default)
#   ChallengeResponseAuthentication yes
#   CheckHostIP yes
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc,blowfish-cbc,cast128-cbc,aes192-cbc,aes256-cbc,arcfour
#   ClearAllForwardings no
#   Compression no
#   CompressionLevel 6
#   ConnectionAttempts 1
#   ConnectTimeout # (no default)
#   ControlMaster no
#   ControlPath  # (no default)
#   ControlPersist no
#   DynamicForward
#   EnableSSHKeysign no
#   EscapeChar ~
#   ExitOnForwardFailure no
#   ForwardAgent no
#   ForwardX11 no
#   ForwardX11Timeout 1200
#   ForwardX11Trusted no
#   XauthLocation xauth # Default is to search $PATH.  It is recommended that a full path be provided.
#   GatewayPorts no
#   GlobalKnownHostsFile /etc/ssh/ssh_known_hosts,/etc/ssh/ssh_known_hosts2
#   GSSAPIAuthentication yes
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   HashKnownHosts no
#   HostbasedAuthentication no
#   HostKeyAlgorithms ecdsa-sha2-nistp256-cert-v01@openssh.com,ecdsa-sha2-nistp384-cert-v01@openssh.com,ecdsa-sha2-nistp521-cert-v01@openssh.com,ssh-rsa-cert-v01@openssh.com,ssh-dss-cert-v01@openssh.com,ssh-rsa-cert-v00@openssh.com,ssh-dss-cert-v00@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,ssh-dss
#   HostKeyAlias # (no default)
#   HostName # (set by command at run-time)
#   IdentitiesOnly no
#   IdentityFile .ssh/id_rsa,.ssh/id_dsa
#   IPQoS lowdelay
#   KbdInteractiveAuthentication yes
#   KbdInteractiveDevices # (no default)
#   KexAlgorithms ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group-exchange-sha1,diffie-hellman-group14-sha1,diffie-hellman-group1-sha1
#   LocalCommand  # (no default)
#   LocalForward  # (no default)
#   LogLevel INFO
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160,hmac-sha1-96,hmac-md5-96,hmac-sha2-256,hmac-sha2-256-96,hmac-sha2-512,hmac-sha2-512-96
#   NoHostAuthenticationForLocalhost no
#   NumberOfPasswordPrompts 3
#   PasswordAuthentication yes
#   PermitLocalCommand no
#   PKCS11Provider # (no default)
#   Port 22
#   PreferredAuthentications gssapi-with-mic,hostbased,publickey,keyboard-interactive,password  # (set by ssh at run-time)
#   Protocol 2
#   ProxyCommand # (no default)
#   PubkeyAuthentication yes
#   RekeyLimit 0
#   RemoteForward # (no default)
#   RequestTTY auto
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   SendEnv # (no default)
#   ServerAliveCountMax 3
#   ServerAliveInterval 0
#   StrictHostKeyChecking ask
#   TCPKeepAlive yes
#   Tunnel no
#   TunnelDevice any:any
#   UsePrivilegedPort no
#   User # (set by command at run-time)
#   UserKnownHostsFile ~/.ssh/known_hosts,~/.ssh/known_hosts2
#   VerifyHostKeyDNS no
#   VisualHostKey no
#   XAuthLocationi xauth
```

### Supported Properties
Viewable on the [Wiki](https://github.com/kkirsche/ssh-config/wiki/Supported-Properties) for easy access and sharing (and avoid keeping this junked up.)

### Meta

#### Version Number

```shell
~ ❯❯❯ ssh-config version
0.0.1
```
