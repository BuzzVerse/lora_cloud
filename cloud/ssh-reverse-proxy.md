# 🤝 SSH reverse proxy

{% code title="/etc/systemd/system/ssh-proxy.service" %}
```bash
[Unit]
Description=SSH tunnel
After=network.target

[Service]
User=debian
RestartSec=5
Restart=always
ExecStart=/usr/bin/autossh -N -M 0 -o "ExitOnForwardFailure=yes" \
                                   -o "ServerAliveInterval=180" \
                                   -o "ServerAliveCountMax=3" \
                                   -o "PubkeyAuthentication=yes" \
                                   -o "PasswordAuthentication=no" \
                                   -i ~/.ssh/klucz \
                                   -R 25565:localhost:22 ubuntu@158.180.60.2

[Install]
WantedBy=multi-user.target
```
{% endcode %}
