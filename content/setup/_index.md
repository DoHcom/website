---
title: "Setup Guide"
date: 2018-05-08T01:36:22+08:00
draft: false
---

We currently provide setup guide on Linux and macOS platforms.

We recommend using [m13253/dns-over-https](https://github.com/m13253/dns-over-https) to access our service. [Other compatible clients](https://github.com/curl/curl/wiki/DNS-over-HTTPS) are also supported.

### Notes

1. We might shut down our service at any time – probably because we run out of our pocket money.

2. We reserve the rights to prevent abuse of our services, including but not limited to: occupying large amount of computing resources, initiating cyberattacks, conducting illegal penetration tests.

3. We regularly keep access logs to monitor service health, and periodically clear them every day.

4. To protect privacy, we do recursive queries with DNSSEC check by ourselves without relying on other public DNS resolvers. That would be much slower, you have been warned.

5. Your IP prefix (/24 for IPv4, /48 for IPv6) is used for retrieving GeoDNS-related results. For `doh-client`, you may use `no_ecs` to opt out.

6. Some domains (especially those hosted on Alibaba DNS) fail to resolve due to connectivity problems. Write to us if it happens. We will forward related quries to Google or CloudFlare’s resolvers.

### For Linux (Ubuntu 18.04)

1. Execute:

    ```
    sudo apt install git golang
    git clone https://github.com/m13253/dns-over-https.git
    cd dns-over-https
    make
    sudo make install
    sudo edit /etc/dns-over-https/doh-client.conf
    ```

2. Change the following lines:

    ```
    upstream_google = [
    ]
    upstream_ietf = [
        "https://dns.dns-over-https.com/dns-query",
    ]
    ```

3. Execute:
    ```
    sudo systemctl stop systemd-resolved
    sudo systemctl start doh-client
    sudo systemctl disable systemd-resolved
    sudo systemctl enable doh-client
    ```

4. Modify your DNS settings (usually with NetworkManager) to `127.0.0.1`.

### For Linux (Ubuntu pre-18.04)

1. Execute:

    ```
    sudo apt install git golang-1.10
    export PATH=$PATH:/usr/lib/go-1.10/bin
    git clone https://github.com/m13253/dns-over-https.git
    cd dns-over-https
    make
    sudo make install
    sudo edit /etc/dns-over-https/doh-client.conf
    ```

2. Change the following lines:

    ```
    upstream_google = [
    ]
    upstream_ietf = [
        "https://dns.dns-over-https.com/dns-query",
    ]
    ```

3. Execute:

    ```
    sudo systemctl start doh-client
    sudo systemctl enable doh-client
    ```

4. Modify your DNS settings (usually with NetworkManager) to `127.0.0.1`.

### For macOS

1. Execute:

    ```
    brew install go
    git clone https://github.com/m13253/dns-over-https.git
    cd dns-over-https
    make
    sudo make install
    open -t /usr/local/etc/dns-over-https/doh-client.conf
    ```

2. Change the following lines:

    ```
    upstream_google = [
    ]
    upstream_ietf = [
        "https://dns.dns-over-https.com/dns-query",
    ]
    ```

3. Execute:

    ```
    sudo launchctl load /Library/LaunchDaemons/doh-client.plist
    ```

4. Modify your DNS settings to `127.0.0.1`.

### Contact

Feel free to write to the “dns” mailbox of “dns-over-https.com” in case of anything you want to tell us.