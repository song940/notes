---
layout: default
title: Ollama
---

# Ollama

![](https://github.com/jmorganca/ollama/assets/3325447/0d0b44e2-8f4a-4e99-9b52-a5c1c741c8f7)

## Install

### Download the `ollama` binary

Ollama is distributed as a self-contained binary. Download it to a directory in your PATH:

```bash
sudo curl -L https://ollama.com/download/ollama-linux-amd64 -o /usr/bin/ollama
sudo chmod +x /usr/bin/ollama
```

### Adding Ollama as a startup service (recommended)

Create a user for Ollama:

```bash
sudo useradd -r -s /bin/false -m -d /usr/share/ollama ollama
```

Create a service file in `/etc/systemd/system/ollama.service`:

```ini
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
Environment=OLLAMA_HOST=0.0.0.0
ExecStart=/usr/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3

[Install]
WantedBy=default.target
```

Then start the service:

```bash
sudo systemctl daemon-reload
sudo systemctl enable ollama
```

### Start Ollama

Start Ollama using `systemd`:

```bash
sudo systemctl start ollama
```

## Using Ollama

```shell
ollama run llama2
ollama run mistral
ollama run yi
```

<https://github.com/ollama/ollama>
<https://blog.inoki.cc/2024/04/16/Ollama-cn/>