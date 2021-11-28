# wirego

`wirego` is a simple script to manage your many Wireguard's profiles


## Installation

Just download `wirego` and save it in a directory of your $PATH, e.g.

```
wget https://raw.githubusercontent.com/francescor/wirego/main/wirego
sudo mv wirego /usr/local/bin
sudo chmod +x /usr/local/bin/wirego
```

## Examples

List all available Wireguard profiles:

`wirego`

Turn on Wireguard profile `/etc/wireguard/myvpn.conf`

`wirego myvpn`

Turn down Wireguard

`wirego down`

Generate the QR code of a profile

`wirego qr`


## Why?

Wireguard tool commands `wg` & `wg-quick` do not get into my head :(  so I've just created this basic script for myself.  
In my daily job I take up and down Wireguard's profile a lot, and some together at the same time, so I do use this 
scrip myself a lot.

Fedora DNS handling is a bit nasty to me: I see I need to execute 

```
sudo systemctl  restart systemd-resolved.service
```
everytime I turn down Wireguard (to remove from `/etc/resolv.conf` the DNS added by the Wireguard VPN), so 
I just added this command once at the end of the script, instead of having to add a `PostDown` in each wg profile.

## Configuration file

An empty configuration file is created in your HOME: `~/.wirego/wirego.profile`

It is useful to store a list of Wireguard profiles you want to take up all together

e.g. with this content in `~/.wirego/wirego.profile`
```
# Ordered list of wireguard profiles to take up with `wirego up`
up_profiles="office1 office2 office3"
```
the command:
```
wirego up
```
will activete all three wireguard profiles

## Notes, requirements, and limitations

It's just a basic script, written for Fedora Linux (v.33, 34), so you may have to adapt it to your o.s.
Feel free to fork and adapt this code, of just suggest changes here.

It requires:
* [Wireguard VPN](https://www.wireguard.com/install/) of course;
* [wireguard-tools](https://git.zx2c4.com/wireguard-tools/about/), so its great `wg` utility;

and Wireguard profiles must be saved into the directory: `/etc/wireguard`

Script is made with the idea of having *only one* Wireguard profile active at a time: so when you turn up a new profile, the active one is taken down.

To generate QR code, install qrencode

```
sudo dnf install qrencode
```
