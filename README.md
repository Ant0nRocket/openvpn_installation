# OpenVPN installation

Steps for setting up a VPN network with OpenVPN.   
'#>' means output you should see during the process.

1. Install dependencies:

```bash
sudo apt install zip ntpdate ntp
```

2. Update time:

```bash
sudo service ntp stop
sudo ntpdate pool.ntp.org
sudo service ntp start
```

3. Create user for CA Server and logon:

```bash
sudo adduser ca
su ca
cd ~
```

4. Download Easy-RSA tool:

```bash
wget https://github.com/OpenVPN/easy-rsa/archive/master.zip
unzip master.zip
cd easy-rsa-master/easyrsa3
```

5. Init PKI (Public Key Infrastructure):

```bash
./easyrsa init-pki
#> init-pki complete; you may now create a CA or requests.
#> Your newly created PKI dir is: /home/ca/easy-rsa-master/easyrsa3/pki

```

6. Building CA:

```bash
./easyrsa build-ca
#> Generating a 2048 bit RSA private key
#> ... [Common Name]
```
Write your [Common Name]. Usualy it is **ca.[domain].**   
If you don't want parovide password on any request add **nopass** (IT's INSECURE!!!):

```bash
./easyrsa build-ca nopass
```

There are two important files on this step:

- ./pki/**ca.crt** 
- ./pki/private/**ca.key**

<u>DO NOT EVER (!!!) show or transfer **ca.key**!</u> File **ca.crt** is public, so you can (and must :)) show it for everyone.