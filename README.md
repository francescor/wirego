# wirego

`wirego` is a basic script to manage your many Wireguard's profiles.


## Installation

Just download `wirego` and save it in a directory of your $PATH, e.g.

```
wget https://raw.githubusercontent.com/francescor/wirego/main/wirego
chmod +x wirego
sudo mv wirego /usr/local/bin
```

## Examples

List all available Wireguard profiles:

`wirego`

Turn on Wireguard profile `/etc/wireguard/myvpn.conf`

`wirego myvpn`

Turn up all Wireguard profiles defined in `~/.wirego/wirego.profile` (prior do taking down all previous active Wireguard profiles)

`wirego up`

Turn down any active Wireguard

`wirego down`

Show the QR code of a profile

`wirego qr`


## Why?

Wireguard tool commands `wg` & `wg-quick` do not get into my head :(  so I've just created this basic script for myself.
I find myself taking up and down differen Wireguard profiles very often, and definitively many at the same time, so I just needed this script myself.

Btw, Fedora DNS handling is a bit nasty to me: I see I need to execute

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
will activete all three wireguard profiles: note that if one or more profiles set the DNS, the last profile will `win`, of course;
at the same time only one profile should have the "catch all" directive: `AllowedIPs = 0.0.0.0/0` but, as you know, you can skip this if you want
to surf the internet with your modem's pulic IP: this is pretty useful when your customers provides you with their Wireguard as a way to give you a public address that allows you to access their web services: you do not want to surf the internet with their IP (just their servers).

## Notes, requirements, and limitations

It's just a basic script, written for Fedora Linux (v.33... 40), so you may have to adapt it to your o.s.
Feel free to fork and adapt this code, of just suggest changes here.

It requires:
* [Wireguard VPN module](https://www.wireguard.com/install/) which is probably already available in your Linux;
* [wireguard-tools](https://www.wireguard.com/install/) (`dnf install wireguard-tools`) that provides its great `wg` utility;
* `sudo`

and Wireguard profiles should be saved into the directory: `/etc/wireguard`

Script is based on the convention that when you activate one profile (or many profiles), all active ones are first taken down.

To generate QR code with `wirego qr` (useful to move your vpn to a mobile phone), you need `qrencode`

```
sudo dnf install qrencode
```
