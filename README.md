<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Install ShadowProxy Client</title>
</head>
<body>
    <h1>Install ShadowProxy Client</h1>

    <h2>Installation Steps</h2>

    <ol>
        <li>Update the package list:</li>
    </ol>

    <pre>
        <code>
sudo apt update
        </code>
    </pre>

    <ol start="2">
        <li>Install Shadowsocks-Libev:</li>
    </ol>

    <pre>
        <code>
sudo apt install shadowsocks-libev -y
        </code>
    </pre>

    <ol start="3">
        <li>Create a daemon user and user group:</li>
    </ol>

    <pre>
        <code>
sudo useradd -r -s /bin/false shadowsocks
sudo groupadd shadowsocks
sudo chown -R shadowsocks:shadowsocks /etc/shadowsocks-libev/
        </code>
    </pre>

    <ol start="4">
        <li>Open the JSON configuration file and add the following properties with values:</li>
    </ol>

    <p>Introduce property fields:</p>

    <ul>
        <li><strong>"server":</strong> The IP address or domain name of the Shadowsocks remote server to which the client should connect. This is the address of the remote Shadowsocks server that the client will use as a proxy.</li>
        <li><strong>"mode":</strong> The operational mode of the Shadowsocks client/server. It typically specifies whether the instance should run as a client or a server. Common modes include "local" (client) and "server" (server).</li>
        <li><strong>"server_port":</strong> The port number on which the Shadowsocks server is listening for incoming connections. The client will connect to this port on the server.</li>
        <li><strong>"local_address":</strong> The local IP address on the client or server where Shadowsocks will listen for incoming connections. It's often set to "127.0.0.1" to listen only on the local machine.</li>
        <li><strong>"local_port":</strong> The port number on the local machine (client or server) where Shadowsocks will listen for incoming connections.</li>
        <li><strong>"nameserver":</strong> The DNS (Domain Name System) server address that the client/server should use for domain name resolution. This can be the IP address of a DNS server.</li>
        <li><strong>"password":</strong> The pre-shared secret or password that is used for authentication and encryption between the client and the server. It's a crucial security parameter.</li>
        <li><strong>"timeout":</strong> The timeout duration in seconds. If no data is transmitted for the specified duration, the connection is considered idle and may be closed.</li>
        <li><strong>"method":</strong> The encryption method or cipher used for securing the communication between the client and server. Common methods include "aes-256-gcm," "chacha20-ietf," etc. It determines how data is encrypted and decrypted.</li>
    </ul>

    <pre>
        <code>
sudo nano /etc/shadowsocks-libev/shadowsocks.json
        </code>
    </pre>

    <pre>
        <code>
{
    "server": "your_server_ip_or_domain",
    "mode": "local",
    "server_port": 8080,
    "local_address": "127.0.0.1",
    "local_port": 1080,
    "nameserver": "DNS_server_ip",
    "password": "your_password",
    "timeout": 300,
    "method": "aes-256-gcm"
}
        </code>
    </pre>

    <ol start="5">
        <li>Test the current configuration:</li>
    </ol>

    <pre>
        <code>
sudo ss-local -c /etc/shadowsocks-libev/shadowsocks.json
        </code>
    </pre>

    <ol start="6">
        <li>If the configuration is successful, create a proxy client daemon by creating a systemd service file:</li>
    </ol>

    <pre>
        <code>
sudo nano /etc/systemd/system/shadowsocks.service
        </code>
    </pre>

    <p>Add the following lines to the service file:</p>

    <pre>
        <code>
[Unit]
Description=Shadowsocks Proxy Client

[Service]
User=shadowsocks
Group=shadowsocks
Type=simple
ExecStart=/usr/bin/ss-local -c /etc/shadowsocks-libev/shadowsocks.json -a shadowsocks -v start
ExecStop=/usr/bin/ss-local -c /etc/shadowsocks-libev/shadowsocks.json -a shadowsocks -v stop

[Install]
WantedBy=multi-user.target
        </code>
    </pre>

    <ol start="7">
        <li>Update daemon services and enable automatic startup:</li>
    </ol>

    <pre>
        <code>
sudo systemctl daemon-reload
sudo systemctl enable shadowsocks.service
        </code>
    </pre>

    <ol start="8">
        <li>Start the Shadowsocks service:</li>
    </ol>

    <pre>
        <code>
sudo systemctl start shadowsocks.service
        </code>
    </pre>

    <ol start="9">
        <li>Verify the service status:</li>
    </ol>

    <pre>
        <code>
         sudo systemctl status shadowsocks.service
        </code>
    </pre>

    <h3>Congratulations! Shadowsocks Proxy Client is now installed and running.</h3>
</body>
</html>
