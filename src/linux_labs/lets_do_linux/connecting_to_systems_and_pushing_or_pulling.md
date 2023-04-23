# Connecting to systems and pushing or pulling files

### Linux Commands to connect to another system

```admonish summary
Connect to the other server and look at the specifics of the ssh connection 🐧 🐧 🐧
```

---

### 1. Check your ip address

~~~admonish example title="Input"
```bash
ssh node01
```
~~~

~~~admonish collapsible=true title="Example Output"
```
controlplane $ ssh node01
Last login: Sun Nov 13 17:27:09 2022 from 10.48.0.33
```
~~~

### 2. Type in exit to return to the original system

~~~admonish example title="Input"
```bash
exit
```
~~~

### 3. Check system uptime and one layer of debug1

~~~admonish example title="Input"
```bash
ssh -v node01 'uptime'
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ ssh -v node01 'uptime'
OpenSSH_8.2p1 Ubuntu-4ubuntu0.5, OpenSSL 1.1.1f  31 Mar 2020
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 19: include /etc/ssh/ssh_config.d/*.conf matched no files
debug1: /etc/ssh/ssh_config line 21: Applying options for *
debug1: Connecting to node01 [172.30.2.2] port 22.
debug1: Connection established.
debug1: identity file /root/.ssh/id_rsa type 0
debug1: identity file /root/.ssh/id_rsa-cert type -1
debug1: identity file /root/.ssh/id_dsa type -1
debug1: identity file /root/.ssh/id_dsa-cert type -1
debug1: identity file /root/.ssh/id_ecdsa type -1
debug1: identity file /root/.ssh/id_ecdsa-cert type -1
debug1: identity file /root/.ssh/id_ecdsa_sk type -1
debug1: identity file /root/.ssh/id_ecdsa_sk-cert type -1
debug1: identity file /root/.ssh/id_ed25519 type -1
debug1: identity file /root/.ssh/id_ed25519-cert type -1
debug1: identity file /root/.ssh/id_ed25519_sk type -1
debug1: identity file /root/.ssh/id_ed25519_sk-cert type -1
debug1: identity file /root/.ssh/id_xmss type -1
debug1: identity file /root/.ssh/id_xmss-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.5
debug1: Remote protocol version 2.0, remote software version OpenSSH_8.2p1 Ubuntu-4ubuntu0.5
debug1: match: OpenSSH_8.2p1 Ubuntu-4ubuntu0.5 pat OpenSSH* compat 0x04000000
debug1: Authenticating to node01:22 as 'root'
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: ecdsa-sha2-nistp256
debug1: kex: server->client cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: kex: client->server cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug1: Server host key: ecdsa-sha2-nistp256 SHA256:tmvetqpbpeuonMk7CexB57k+hK4t1129IaLp/W2TMs0
debug1: Host 'node01' is known and matches the ECDSA host key.
debug1: Found key in /root/.ssh/known_hosts:5
debug1: rekey out after 134217728 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug1: SSH2_MSG_NEWKEYS received
debug1: rekey in after 134217728 blocks
debug1: Will attempt key: /root/.ssh/id_rsa RSA SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug1: Will attempt key: /root/.ssh/id_dsa 
debug1: Will attempt key: /root/.ssh/id_ecdsa 
debug1: Will attempt key: /root/.ssh/id_ecdsa_sk 
debug1: Will attempt key: /root/.ssh/id_ed25519 
debug1: Will attempt key: /root/.ssh/id_ed25519_sk 
debug1: Will attempt key: /root/.ssh/id_xmss 
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_input_ext_info: server-sig-algs=<ssh-ed25519,sk-ssh-ed25519@openssh.com,ssh-rsa,rsa-sha2-256,rsa-sha2-512,ssh-dss,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ecdsa-sha2-nistp256@openssh.com>
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug1: Authentications that can continue: publickey,password,keyboard-interactive
debug1: Next authentication method: publickey
debug1: Offering public key: /root/.ssh/id_rsa RSA SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug1: Server accepts key: /root/.ssh/id_rsa RSA SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug1: Authentication succeeded (publickey).
Authenticated to node01 ([172.30.2.2]:22).
debug1: channel 0: new [client-session]
debug1: Requesting no-more-sessions@openssh.com
debug1: Entering interactive session.
debug1: pledge: network
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
debug1: Remote: /root/.ssh/authorized_keys:2: key options: agent-forwarding port-forwarding pty user-rc x11-forwarding
debug1: Remote: /root/.ssh/authorized_keys:2: key options: agent-forwarding port-forwarding pty user-rc x11-forwarding
debug1: Sending environment.
debug1: Sending command: uptime
 13:15:22 up 37 min,  1 user,  load average: 0.01, 0.05, 0.11
debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
debug1: client_input_channel_req: channel 0 rtype eow@openssh.com reply 0
debug1: channel 0: free: client-session, nchannels 1
Transferred: sent 2820, received 3088 bytes, in 0.0 seconds
Bytes per second: sent 60469.7, received 66216.5
debug1: Exit status 0
```
~~~

### 4. What additional information was shown with the -v option? (debug1)

~~~admonish example title="Input"
```bash
ssh -vv node01 'uptime'
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ ssh -vv node01 'uptime'
OpenSSH_8.2p1 Ubuntu-4ubuntu0.5, OpenSSL 1.1.1f  31 Mar 2020
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 19: include /etc/ssh/ssh_config.d/*.conf matched no files
debug1: /etc/ssh/ssh_config line 21: Applying options for *
debug2: resolving "node01" port 22
debug2: ssh_connect_direct
debug1: Connecting to node01 [172.30.2.2] port 22.
debug1: Connection established.
debug1: identity file /root/.ssh/id_rsa type 0
debug1: identity file /root/.ssh/id_rsa-cert type -1
debug1: identity file /root/.ssh/id_dsa type -1
debug1: identity file /root/.ssh/id_dsa-cert type -1
debug1: identity file /root/.ssh/id_ecdsa type -1
debug1: identity file /root/.ssh/id_ecdsa-cert type -1
debug1: identity file /root/.ssh/id_ecdsa_sk type -1
debug1: identity file /root/.ssh/id_ecdsa_sk-cert type -1
debug1: identity file /root/.ssh/id_ed25519 type -1
debug1: identity file /root/.ssh/id_ed25519-cert type -1
debug1: identity file /root/.ssh/id_ed25519_sk type -1
debug1: identity file /root/.ssh/id_ed25519_sk-cert type -1
debug1: identity file /root/.ssh/id_xmss type -1
debug1: identity file /root/.ssh/id_xmss-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.5
debug1: Remote protocol version 2.0, remote software version OpenSSH_8.2p1 Ubuntu-4ubuntu0.5
debug1: match: OpenSSH_8.2p1 Ubuntu-4ubuntu0.5 pat OpenSSH* compat 0x04000000
debug2: fd 3 setting O_NONBLOCK
debug1: Authenticating to node01:22 as 'root'
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug2: local client KEXINIT proposal
debug2: KEX algorithms: curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group14-sha256,ext-info-c
debug2: host key algorithms: ecdsa-sha2-nistp256-cert-v01@openssh.com,ecdsa-sha2-nistp384-cert-v01@openssh.com,ecdsa-sha2-nistp521-cert-v01@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ecdsa-sha2-nistp256-cert-v01@openssh.com,ssh-ed25519-cert-v01@openssh.com,sk-ssh-ed25519-cert-v01@openssh.com,rsa-sha2-512-cert-v01@openssh.com,rsa-sha2-256-cert-v01@openssh.com,ssh-rsa-cert-v01@openssh.com,sk-ecdsa-sha2-nistp256@openssh.com,ssh-ed25519,sk-ssh-ed25519@openssh.com,rsa-sha2-512,rsa-sha2-256,ssh-rsa
debug2: ciphers ctos: chacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com
debug2: ciphers stoc: chacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com
debug2: MACs ctos: umac-64-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,hmac-sha2-256,hmac-sha2-512,hmac-sha1
debug2: MACs stoc: umac-64-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,hmac-sha2-256,hmac-sha2-512,hmac-sha1
debug2: compression ctos: none,zlib@openssh.com,zlib
debug2: compression stoc: none,zlib@openssh.com,zlib
debug2: languages ctos: 
debug2: languages stoc: 
debug2: first_kex_follows 0 
debug2: reserved 0 
debug2: peer server KEXINIT proposal
debug2: KEX algorithms: curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group14-sha256
debug2: host key algorithms: rsa-sha2-512,rsa-sha2-256,ssh-rsa,ecdsa-sha2-nistp256,ssh-ed25519
debug2: ciphers ctos: chacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com
debug2: ciphers stoc: chacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com
debug2: MACs ctos: umac-64-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,hmac-sha2-256,hmac-sha2-512,hmac-sha1
debug2: MACs stoc: umac-64-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,hmac-sha2-256,hmac-sha2-512,hmac-sha1
debug2: compression ctos: none,zlib@openssh.com
debug2: compression stoc: none,zlib@openssh.com
debug2: languages ctos: 
debug2: languages stoc: 
debug2: first_kex_follows 0 
debug2: reserved 0 
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: ecdsa-sha2-nistp256
debug1: kex: server->client cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: kex: client->server cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug1: Server host key: ecdsa-sha2-nistp256 SHA256:tmvetqpbpeuonMk7CexB57k+hK4t1129IaLp/W2TMs0
debug1: Host 'node01' is known and matches the ECDSA host key.
debug1: Found key in /root/.ssh/known_hosts:5
debug2: set_newkeys: mode 1
debug1: rekey out after 134217728 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug1: SSH2_MSG_NEWKEYS received
debug2: set_newkeys: mode 0
debug1: rekey in after 134217728 blocks
debug1: Will attempt key: /root/.ssh/id_rsa RSA SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug1: Will attempt key: /root/.ssh/id_dsa 
debug1: Will attempt key: /root/.ssh/id_ecdsa 
debug1: Will attempt key: /root/.ssh/id_ecdsa_sk 
debug1: Will attempt key: /root/.ssh/id_ed25519 
debug1: Will attempt key: /root/.ssh/id_ed25519_sk 
debug1: Will attempt key: /root/.ssh/id_xmss 
debug2: pubkey_prepare: done
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_input_ext_info: server-sig-algs=<ssh-ed25519,sk-ssh-ed25519@openssh.com,ssh-rsa,rsa-sha2-256,rsa-sha2-512,ssh-dss,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ecdsa-sha2-nistp256@openssh.com>
debug2: service_accept: ssh-userauth
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug1: Authentications that can continue: publickey,password,keyboard-interactive
debug1: Next authentication method: publickey
debug1: Offering public key: /root/.ssh/id_rsa RSA SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug2: we sent a publickey packet, wait for reply
debug1: Server accepts key: /root/.ssh/id_rsa RSA SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug1: Authentication succeeded (publickey).
Authenticated to node01 ([172.30.2.2]:22).
debug1: channel 0: new [client-session]
debug2: channel 0: send open
debug1: Requesting no-more-sessions@openssh.com
debug1: Entering interactive session.
debug1: pledge: network
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
debug1: Remote: /root/.ssh/authorized_keys:2: key options: agent-forwarding port-forwarding pty user-rc x11-forwarding
debug1: Remote: /root/.ssh/authorized_keys:2: key options: agent-forwarding port-forwarding pty user-rc x11-forwarding
debug2: channel_input_open_confirmation: channel 0: callback start
debug2: fd 3 setting TCP_NODELAY
debug2: client_session2_setup: id 0
debug1: Sending environment.
debug1: Sending command: uptime
debug2: channel 0: request exec confirm 1
debug2: channel_input_open_confirmation: channel 0: callback done
debug2: channel 0: open confirm rwindow 0 rmax 32768
debug2: channel 0: rcvd adjust 2097152
debug2: channel_input_status_confirm: type 99 id 0
debug2: exec request accepted on channel 0
debug2: channel 0: rcvd eof
debug2: channel 0: output open -> drain
 13:16:53 up 39 min,  1 user,  load average: 0.00, 0.03, 0.10
debug2: channel 0: obuf empty
debug2: channel 0: chan_shutdown_write (i0 o1 sock -1 wfd 5 efd 6 [write])
debug2: channel 0: output drain -> closed
debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
debug1: client_input_channel_req: channel 0 rtype eow@openssh.com reply 0
debug2: channel 0: rcvd eow
debug2: channel 0: chan_shutdown_read (i0 o3 sock -1 wfd 4 efd 6 [write])
debug2: channel 0: input open -> closed
debug2: channel 0: rcvd close
debug2: channel 0: almost dead
debug2: channel 0: gc: notify user
debug2: channel 0: gc: user detached
debug2: channel 0: send close
debug2: channel 0: is dead
debug2: channel 0: garbage collecting
debug1: channel 0: free: client-session, nchannels 1
Transferred: sent 2820, received 3088 bytes, in 0.0 seconds
Bytes per second: sent 56551.2, received 61925.6
debug1: Exit status 0
```
~~~

### 5. What additional information was shown with the -vv option? (debug2)

~~~admonish example title="Input"
```bash
ssh -vvv node01 'uptime'
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ ssh -vvv node01 'uptime' 
OpenSSH_8.2p1 Ubuntu-4ubuntu0.5, OpenSSL 1.1.1f  31 Mar 2020
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 19: include /etc/ssh/ssh_config.d/*.conf matched no files
debug1: /etc/ssh/ssh_config line 21: Applying options for *
debug2: resolving "node01" port 22
debug2: ssh_connect_direct
debug1: Connecting to node01 [172.30.2.2] port 22.
debug1: Connection established.
debug1: identity file /root/.ssh/id_rsa type 0
debug1: identity file /root/.ssh/id_rsa-cert type -1
debug1: identity file /root/.ssh/id_dsa type -1
debug1: identity file /root/.ssh/id_dsa-cert type -1
debug1: identity file /root/.ssh/id_ecdsa type -1
debug1: identity file /root/.ssh/id_ecdsa-cert type -1
debug1: identity file /root/.ssh/id_ecdsa_sk type -1
debug1: identity file /root/.ssh/id_ecdsa_sk-cert type -1
debug1: identity file /root/.ssh/id_ed25519 type -1
debug1: identity file /root/.ssh/id_ed25519-cert type -1
debug1: identity file /root/.ssh/id_ed25519_sk type -1
debug1: identity file /root/.ssh/id_ed25519_sk-cert type -1
debug1: identity file /root/.ssh/id_xmss type -1
debug1: identity file /root/.ssh/id_xmss-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.5
debug1: Remote protocol version 2.0, remote software version OpenSSH_8.2p1 Ubuntu-4ubuntu0.5
debug1: match: OpenSSH_8.2p1 Ubuntu-4ubuntu0.5 pat OpenSSH* compat 0x04000000
debug2: fd 3 setting O_NONBLOCK
debug1: Authenticating to node01:22 as 'root'
debug3: hostkeys_foreach: reading file "/root/.ssh/known_hosts"
debug3: record_hostkey: found key type ECDSA in file /root/.ssh/known_hosts:5
debug3: load_hostkeys: loaded 1 keys from node01
debug3: order_hostkeyalgs: prefer hostkeyalgs: ecdsa-sha2-nistp256-cert-v01@openssh.com,ecdsa-sha2-nistp384-cert-v01@openssh.com,ecdsa-sha2-nistp521-cert-v01@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521
debug3: send packet: type 20
debug1: SSH2_MSG_KEXINIT sent
debug3: receive packet: type 20
debug1: SSH2_MSG_KEXINIT received
debug2: local client KEXINIT proposal
debug2: KEX algorithms: curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group14-sha256,ext-info-c
debug2: host key algorithms: ecdsa-sha2-nistp256-cert-v01@openssh.com,ecdsa-sha2-nistp384-cert-v01@openssh.com,ecdsa-sha2-nistp521-cert-v01@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ecdsa-sha2-nistp256-cert-v01@openssh.com,ssh-ed25519-cert-v01@openssh.com,sk-ssh-ed25519-cert-v01@openssh.com,rsa-sha2-512-cert-v01@openssh.com,rsa-sha2-256-cert-v01@openssh.com,ssh-rsa-cert-v01@openssh.com,sk-ecdsa-sha2-nistp256@openssh.com,ssh-ed25519,sk-ssh-ed25519@openssh.com,rsa-sha2-512,rsa-sha2-256,ssh-rsa
debug2: ciphers ctos: chacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com
debug2: ciphers stoc: chacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com
debug2: MACs ctos: umac-64-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,hmac-sha2-256,hmac-sha2-512,hmac-sha1
debug2: MACs stoc: umac-64-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,hmac-sha2-256,hmac-sha2-512,hmac-sha1
debug2: compression ctos: none,zlib@openssh.com,zlib
debug2: compression stoc: none,zlib@openssh.com,zlib
debug2: languages ctos: 
debug2: languages stoc: 
debug2: first_kex_follows 0 
debug2: reserved 0 
debug2: peer server KEXINIT proposal
debug2: KEX algorithms: curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,diffie-hellman-group14-sha256
debug2: host key algorithms: rsa-sha2-512,rsa-sha2-256,ssh-rsa,ecdsa-sha2-nistp256,ssh-ed25519
debug2: ciphers ctos: chacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com
debug2: ciphers stoc: chacha20-poly1305@openssh.com,aes128-ctr,aes192-ctr,aes256-ctr,aes128-gcm@openssh.com,aes256-gcm@openssh.com
debug2: MACs ctos: umac-64-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,hmac-sha2-256,hmac-sha2-512,hmac-sha1
debug2: MACs stoc: umac-64-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-64@openssh.com,umac-128@openssh.com,hmac-sha2-256,hmac-sha2-512,hmac-sha1
debug2: compression ctos: none,zlib@openssh.com
debug2: compression stoc: none,zlib@openssh.com
debug2: languages ctos: 
debug2: languages stoc: 
debug2: first_kex_follows 0 
debug2: reserved 0 
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: ecdsa-sha2-nistp256
debug1: kex: server->client cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: kex: client->server cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug3: send packet: type 30
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug3: receive packet: type 31
debug1: Server host key: ecdsa-sha2-nistp256 SHA256:tmvetqpbpeuonMk7CexB57k+hK4t1129IaLp/W2TMs0
debug3: hostkeys_foreach: reading file "/root/.ssh/known_hosts"
debug3: record_hostkey: found key type ECDSA in file /root/.ssh/known_hosts:5
debug3: load_hostkeys: loaded 1 keys from node01
debug3: hostkeys_foreach: reading file "/root/.ssh/known_hosts"
debug3: record_hostkey: found key type ECDSA in file /root/.ssh/known_hosts:6
debug3: load_hostkeys: loaded 1 keys from 172.30.2.2
debug1: Host 'node01' is known and matches the ECDSA host key.
debug1: Found key in /root/.ssh/known_hosts:5
debug3: send packet: type 21
debug2: set_newkeys: mode 1
debug1: rekey out after 134217728 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug3: receive packet: type 21
debug1: SSH2_MSG_NEWKEYS received
debug2: set_newkeys: mode 0
debug1: rekey in after 134217728 blocks
debug1: Will attempt key: /root/.ssh/id_rsa RSA SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug1: Will attempt key: /root/.ssh/id_dsa 
debug1: Will attempt key: /root/.ssh/id_ecdsa 
debug1: Will attempt key: /root/.ssh/id_ecdsa_sk 
debug1: Will attempt key: /root/.ssh/id_ed25519 
debug1: Will attempt key: /root/.ssh/id_ed25519_sk 
debug1: Will attempt key: /root/.ssh/id_xmss 
debug2: pubkey_prepare: done
debug3: send packet: type 5
debug3: receive packet: type 7
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_input_ext_info: server-sig-algs=<ssh-ed25519,sk-ssh-ed25519@openssh.com,ssh-rsa,rsa-sha2-256,rsa-sha2-512,ssh-dss,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ecdsa-sha2-nistp256@openssh.com>
debug3: receive packet: type 6
debug2: service_accept: ssh-userauth
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug3: send packet: type 50
debug3: receive packet: type 51
debug1: Authentications that can continue: publickey,password,keyboard-interactive
debug3: start over, passed a different list publickey,password,keyboard-interactive
debug3: preferred gssapi-with-mic,publickey,keyboard-interactive,password
debug3: authmethod_lookup publickey
debug3: remaining preferred: keyboard-interactive,password
debug3: authmethod_is_enabled publickey
debug1: Next authentication method: publickey
debug1: Offering public key: /root/.ssh/id_rsa RSA SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug3: send packet: type 50
debug2: we sent a publickey packet, wait for reply
debug3: receive packet: type 60
debug1: Server accepts key: /root/.ssh/id_rsa RSA SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug3: sign_and_send_pubkey: RSA SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug3: sign_and_send_pubkey: signing using rsa-sha2-512 SHA256:q90lhwtJI0plO0gcnYrhjqpIMS8fzsHyMGAga1nRElQ
debug3: send packet: type 50
debug3: receive packet: type 52
debug1: Authentication succeeded (publickey).
Authenticated to node01 ([172.30.2.2]:22).
debug1: channel 0: new [client-session]
debug3: ssh_session2_open: channel_new: 0
debug2: channel 0: send open
debug3: send packet: type 90
debug1: Requesting no-more-sessions@openssh.com
debug3: send packet: type 80
debug1: Entering interactive session.
debug1: pledge: network
debug3: receive packet: type 80
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
debug3: receive packet: type 4
debug1: Remote: /root/.ssh/authorized_keys:2: key options: agent-forwarding port-forwarding pty user-rc x11-forwarding
debug3: receive packet: type 4
debug1: Remote: /root/.ssh/authorized_keys:2: key options: agent-forwarding port-forwarding pty user-rc x11-forwarding
debug3: receive packet: type 91
debug2: channel_input_open_confirmation: channel 0: callback start
debug2: fd 3 setting TCP_NODELAY
debug3: ssh_packet_set_tos: set IP_TOS 0x08
debug2: client_session2_setup: id 0
debug1: Sending environment.
debug3: Ignored env SHELL
debug3: Ignored env PWD
debug3: Ignored env LOGNAME
debug3: Ignored env HOME
debug3: Ignored env LS_COLORS
debug3: Ignored env SSH_CONNECTION
debug3: Ignored env LESSCLOSE
debug3: Ignored env TERM
debug3: Ignored env LESSOPEN
debug3: Ignored env USER
debug3: Ignored env SHLVL
debug3: Ignored env PS1
debug3: Ignored env SSH_CLIENT
debug3: Ignored env PATH
debug3: Ignored env MAIL
debug3: Ignored env DEBIAN_FRONTEND
debug3: Ignored env OLDPWD
debug3: Ignored env _
debug1: Sending command: uptime
debug2: channel 0: request exec confirm 1
debug3: send packet: type 98
debug2: channel_input_open_confirmation: channel 0: callback done
debug2: channel 0: open confirm rwindow 0 rmax 32768
debug2: channel 0: rcvd adjust 2097152
debug3: receive packet: type 99
debug2: channel_input_status_confirm: type 99 id 0
debug2: exec request accepted on channel 0
 13:18:35 up 40 min,  1 user,  load average: 0.00, 0.02, 0.08
debug3: receive packet: type 96
debug2: channel 0: rcvd eof
debug2: channel 0: output open -> drain
debug2: channel 0: obuf empty
debug2: channel 0: chan_shutdown_write (i0 o1 sock -1 wfd 5 efd 6 [write])
debug2: channel 0: output drain -> closed
debug3: receive packet: type 98
debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
debug3: receive packet: type 98
debug1: client_input_channel_req: channel 0 rtype eow@openssh.com reply 0
debug2: channel 0: rcvd eow
debug2: channel 0: chan_shutdown_read (i0 o3 sock -1 wfd 4 efd 6 [write])
debug2: channel 0: input open -> closed
debug3: receive packet: type 97
debug2: channel 0: rcvd close
debug3: channel 0: will not send data after close
debug2: channel 0: almost dead
debug2: channel 0: gc: notify user
debug2: channel 0: gc: user detached
debug2: channel 0: send close
debug3: send packet: type 97
debug2: channel 0: is dead
debug2: channel 0: garbage collecting
debug1: channel 0: free: client-session, nchannels 1
debug3: channel 0: status: The following connections are open:
  #0 client-session (t4 r0 i3/0 o3/0 e[write]/0 fd -1/-1/6 sock -1 cc -1)

debug3: send packet: type 1
debug3: fd 1 is not O_NONBLOCK
Transferred: sent 2820, received 3088 bytes, in 0.1 seconds
Bytes per second: sent 47824.7, received 52369.8
debug1: Exit status 0
```
~~~

#### 💬 What additional information was shown with the -vvv option? (debug3)

#### 💬 So we looked at a ssh connection over to node01. You should note that the keys are bing used and that is why no password was asked to connect. We'll explore that more shortly.

```text,editable
// Did you notice any differences?


```

---

### Linux Commands to push and pull files

```admonish summary
🐧 scp is always "from" "to" on the command line, so the syntax is: `scp sourcetarget destinationtarget`

🐧 Push the `/root/motd` file over to node01 at location `/etc/motd` and then log in to verify that the file has been pushed

🐧 Pull `/etc/crontab` from node01 to controlplane as file `/tmp/node01.crontab`
```

💬 Let's push and pull files around to test scp of the systems 🐧 🐧 🐧

### 6. Verify the file you have at `/root/motd`

~~~admonish example title="Input"
```bash
cksum /root/motd
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ cksum /root/motd
37673703 669 /root/motd
```
~~~

### 7. Copy over the `/root/motd` to `node01:/etc/motd`

~~~admonish example title="Input"
```bash
scp /root/motd node01:/etc/motd
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ scp /root/motd node01:/etc/motd
motd                                                  100%  669 506.9KB/s   00:00
```
~~~

#### 💬 You get to see information about how long it took to push the file

### 8. Let's ssh over and see our MOTD

~~~admonish example title="Input"
```bash
timeout 1 ssh node01
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ timeout 1 ssh node01
Last login: Thu Apr 20 13:34:00 2023 from 10.244.4.238
 .----------------.  .----------------.  .----------------.
| .--------------. || .--------------. || .--------------. |
| |  ________    | || |  _________   | || | ____   ____  | |
| | |_   ___ `.  | || | |_   ___  |  | || ||_  _| |_  _| | |
| |   | |   `. \ | || |   | |_  \_|  | || |  \ \   / /   | |
| |   | |    | | | || |   |  _|  _   | || |   \ \ / /    | |
| |  _| |___.' / | || |  _| |___/ |  | || |    \ ' /     | |
| | |________.'  | || | |_________|  | || |     \_/      | |
| |              | || |              | || |              | |
| '--------------' || '--------------' || '--------------' |
 '----------------'  '----------------'  '----------------'
node01 $
```
~~~

#### 💬 Let's verify the file exactly the size we think it is over there

### 9. We can see them, so we'll set that to yes.

~~~admonish example title="Input"
```bash
ssh node01 'cksum /etc/motd'
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ ssh node01 'cksum /etc/motd'
37673703 669 /etc/motd
```
~~~

#### 💬 You should now both see the motd as you log in, as well as seeing the cksum matches what you did in step 1.

#### 💬 Now we have config files that we need to pull and give to the vendor. Let's pull those logs back over to this server from node01

### 10. Verify cksum of /etc/crontab file

~~~admonish example title="Input"
```bash
ssh node01 'cksum /etc/crontab'
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ ssh node01 'cksum /etc/crontab'
638366506 1042 /etc/crontab
```
~~~

### 11. Pull file over to `/tmp/node01.crontab` from node01

~~~admonish example title="Input"
```bash
scp node01:/etc/crontab /tmp/node01.crontab
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ scp node01:/etc/crontab /tmp/node01.crontab
crontab                                               100% 1042     1.1MB/s   00:00    
```
~~~

### 12. So now that you've pulled the file over, verify that it's exactly the same as you just saw it

~~~admonish example title="Input"
```bash
cksum /tmp/node01.crontab
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ cksum /tmp/node01.crontab
638366506 1042 /tmp/node01.crontab
```
~~~

# Look at you, learning Linux! You ssh-ed into servers and pushed or pulled files as needed! 🐧

Next up: [Screen Commands and persistent connections](./screen_commands_and_persistent_connections.md)
