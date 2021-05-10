# wirego
`wirego` is a simple bash script to manage your Wireguard profiles

# why?

Wireguard command `wg`, with it's rulws, does not get into my mind :(  so I just create this basic script for myself

# Notes an limitation

It's just a basic script, written for Fedora Linux (v.33), so you may have to adapt to your o.s.

# Installation

Just download `wirego` and save it in a directory of your $PATH, e.g.

```
wget https://raw.githubusercontent.com/francescor/wirego/main/wirego
sudo mv wirego /usr/local/bin
sudo chmod +x /usr/local/bin/wirego
```

Wireguard profiles must be save into the directory: `/etc/wireguard`

# Examples

List all available Wireguard profiles:

`wirego`

Turn on wireguard profile `/etc/wireguard/myvpn.conf`

`wirego myvpn`

Turn off wireguard

`wirego down`

