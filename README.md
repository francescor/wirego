# wirego

`wirego` is a simple script to manage your laptop many Wireguard profiles


# why?

Wireguard command `wg`, with it's rules, does not get into my mind :(  so I've just created this basic script for myself.

Fedora DNS handling is a bit nasty to me: I see I need to execute 

```
sudo systemctl  restart systemd-resolved.service
```
everytime I turn down Wireguard (to remove from `/etc/resolv.conf` the DNS added by the Wireguard VPN), so 
I just added this command once at the end of the script, instead of having to add a `PostDown` in each wg profile.


# Notes, requirements, and limitations

It's just a basic script, written for Fedora Linux (v.33), so you may have to adapt it to your o.s.
Feel free to fork and adapt this code, of just suggest changes here.

It requires [Wireguard VPN](https://www.wireguard.com/install/) of course, and Wireguard profiles must be saved into the directory: `/etc/wireguard`


Script is made with the idea of having *only one* wireguard profile active at a time: so when you turn up a new profile, the active one is taken down.



# Installation

Just download `wirego` and save it in a directory of your $PATH, e.g.

```
wget https://raw.githubusercontent.com/francescor/wirego/main/wirego
sudo mv wirego /usr/local/bin
sudo chmod +x /usr/local/bin/wirego
```

# Examples

List all available Wireguard profiles:

`wirego`

Turn on wireguard profile `/etc/wireguard/myvpn.conf`

`wirego myvpn`

Turn off wireguard

`wirego down`

