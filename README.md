# plex2shell_pcap
pcap artifacts for plex2shell exploitation

## As of Oct 17th, 2026, this is being exploited in the wild but pcaps with name containing "lab" are from lab testing!!

regarding in the wild exploitation: https://www.boredhackerblog.info/2026/10/plex-vulnerabilities-being-exploited-in.html

Info: https://zmain.info/blog/plex2shell

Associated CVEs:
- CVE-2026-96652
- CVE-2026-96654
- CVE-2026-96655
- CVE-2026-96656

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

pcaps:
- plex2shell_lab_filtered.pcap - interactive rev shell
- plex2shell_lab_one_shot_filtered.pcap - one shot id and hostname i think
- plex2shell_lab_one_shot_2_filtered.pcap - one shot id, hostname, and cat passwd iirc

I don't think --exec or interactive matter too much for detection part. 

from exploit code, these ports and domain being used can always be modified (alongside with many other things like file names etc obv...):
```
    attacker_host = "127.0.0.1.%s.sslip.io" % args.attacker_ip.replace(".", "-")
    token_port, carrier_port, lport = 8952, 8933, 9001
```

Screenshots:

<img width="1408" height="575" alt="image" src="https://github.com/user-attachments/assets/668a4acf-e548-440a-890e-6edb40ee87e6" />

Process tree (of me running sleep via interactive rev shell)

<img width="686" height="64" alt="image" src="https://github.com/user-attachments/assets/15489fcf-27da-47d2-ba4c-abc1fe832397" />


Screenshots from wireshark:

<img width="989" height="363" alt="image" src="https://github.com/user-attachments/assets/356f3944-f7fa-4bc3-aa70-e8ff26006bd8" />

<img width="985" height="535" alt="image" src="https://github.com/user-attachments/assets/afc51824-dd03-4ec9-a7a4-e28a94b4b501" />

<img width="985" height="316" alt="image" src="https://github.com/user-attachments/assets/17a6450b-306e-49bc-8714-740ea428829d" />

<img width="985" height="389" alt="image" src="https://github.com/user-attachments/assets/5ea28d27-59c9-4341-ba00-ccf130cbbfe6" />

<img width="985" height="588" alt="image" src="https://github.com/user-attachments/assets/4c5075ea-dc09-4aee-b82c-4a2463a87b62" />

<img width="985" height="671" alt="image" src="https://github.com/user-attachments/assets/fd2db76f-b271-48c7-834b-29c814142081" />


