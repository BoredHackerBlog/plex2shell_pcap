# plex2shell_pcap
pcap artifacts for plex2shell exploitation

## As of Oct 17th, 2026, this is being exploited in the wild but pcaps with name containing "lab" are from lab testing!!

Info: https://zmain.info/blog/plex2shell

Exploit/POC: https://github.com/code-zm/plex2shell

Target: Docker image: linuxserver/plex:1.42.2 10.98.178.40

Attacker: 10.98.178.28

Target docker-compose.yml: 
```
---
services:
  plex:
    image: linuxserver/plex:1.42.2
    container_name: plex
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - VERSION=docker
    volumes:
      - ./plex/library:/config
      - ./tvseries:/tv
      - ./movies:/movies
    restart: unless-stopped
```

<img width="1408" height="575" alt="image" src="https://github.com/user-attachments/assets/668a4acf-e548-440a-890e-6edb40ee87e6" />

Process tree (of me running sleep via interactive rev shell)

<img width="686" height="64" alt="image" src="https://github.com/user-attachments/assets/15489fcf-27da-47d2-ba4c-abc1fe832397" />
