# VPN to SOCKS

Turn WireGuard connections into SOCKS5 proxies for use with browsers, curl commands and more.

This repository is basically just a docker-compose file that glues two images together:

- [linuxserver/wireguard](https://hub.docker.com/r/linuxserver/wireguard)
- [serjs/go-socks5-proxy](https://hub.docker.com/r/serjs/go-socks5-proxy)

With WireGuard connections exposed as SOCKS proxies, one can easily use multiple simultaneous VPN connections at the same time. This also allows VPN connection sharing by running the proxy on a shared server.

## How To Use

First, put your WireGuard configuration file(s) (usually with `.conf` extension) into the `vpn` folder and rename it to `vpn.conf`.

Then, set the host port (`PROXY_PORT`) on which the SOCKS proxy is exposed by editing the `.env` file.

Finally, just run the command:

```sh
docker compose up -d
```

To test your setup, simply run (replace `PROXY_PORT` with your proxy port number):

```sh
curl ifconfig.me -x "socks5://localhost:PROXY_PORT"
```

## License

[MIT](./LICENSE)
