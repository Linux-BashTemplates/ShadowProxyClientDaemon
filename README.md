 <h1>Install ShadowProxy Client</h1>

    <h2>Installation Steps</h2>

    <ol>
        <li>
            <p>Update your package list:</p>
            <pre><code>sudo apt update</code></pre>
        </li>
        <li>
            <p>Install Shadowsocks-Libev:</p>
            <pre><code>sudo apt install shadowsocks-libev -y</code></pre>
        </li>
        <li>
            <p>Create a daemon user and user group:</p>
            <pre><code>
sudo useradd -r -s /bin/false shadowsocks
sudo groupadd shadowsocks
sudo chown -R shadowsocks:shadowsocks /etc/shadowsocks-libev/
            </code></pre>
        </li>
        <li>
            <p>Open the JSON configuration file and add the following properties with their respective values:</p>
            <ul>
                <li>
                    <p><strong>"server":</strong> The IP address or domain name of the Shadowsocks remote server to which the client should connect. This is the address of the remote Shadowsocks server that the client will use as a proxy.</p>
                </li>
                <li>
                    <p><strong>"mode":</strong> The operational mode of the Shadowsocks client/server. It typically specifies whether the instance should run as a client or a server. Common modes include "local" (client) and "server" (server).</p>
                </li>
                <li>
                    <p><strong>"server_port":</strong> The port number on which the Shadowsocks server is listening for incoming connections. The client will connect to this port on the server.</p>
                </li>
                <li>
                    <p><strong>"local_address":</strong> The local IP address on the client or server where Shadowsocks will listen for incoming connections. It's often set to "127.0.0.1" to listen only on the local machine.</p>
                </li>
                <li>
                    <p><strong>"local_port":</strong> The port number on the local machine where Shadowsocks will listen for incoming connections.</p>
                </li>
                <li>
                    <p><strong>"nameserver":</strong> The DNS (Domain Name System) server address that the client/server should use for domain name resolution. This can be the IP address of a DNS server.</p>
                </li>
                <li>
                    <p><strong>"password":</strong> The pre-shared secret or password that is used for authentication and encryption between the client and the server. It's a crucial security parameter.</p>
                </li>
                <li>
                    <p><strong>"timeout":</strong> The timeout duration in seconds. If no data is transmitted for the specified duration, the connection is considered idle and may be closed.</p>
                </li>
                <li>
                    <p><strong>"method":</strong> The encryption method or cipher used for securing the communication between the client and server. Common methods include "aes-256-gcm," "chacha20-ietf," etc. It determines how data is encrypted and decrypted.</p>
                </li>
            </ul>
            <pre><code>sudo nano /etc/shadowsocks-libev/shadowsocks.json</code></pre>
            <pre><code>
{
    "server": "",
    "mode": "",
    "server_port": ,
    "local_address": "",
    "local_port": ,
    "nameserver": "",
    "password": "",
    "timeout": ,
    "method": ""
}
            </code></pre>
        </li>
        <li>
            <p>Try to run the current configuration:</p>
            <pre><code>sudo ss-local -c /etc/shadowsocks-libev/shadowsocks.json</code></pre>
        </li>
        <li>
            <p>If the configuration is successful, try creating a proxy client daemon:</p>
            <pre><code>
sudo nano /etc/systemd/system/shadosocks.service
            </code></pre>
        </li>
        <li>
            <p>Update daemon services, run and add to autoload:</p>
            <pre><code>
sudo systemctl daemon-reload
sudo systemctl run shadowsocks.service
sudo systemctl status shadowsocks.service
            </code></pre>
        </li>
    </ol>

    <p>Congratulations! Shadowsocks Proxy Client is now installed and running.</p>
