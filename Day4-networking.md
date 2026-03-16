# Day 4 – Linux Networking

## Check IP Address

ip a

Example

inet 192.168.x.x/24

## Types of IP

127.0.0.1 → loopback (your computer)

192.168.x.x → private network IP

Public IP → internet facing address

Server IP → remote server address

## Ping

Test connectivity

ping google.com

## Curl

Fetch website response

curl google.com

Used to test servers and APIs.

## Open Ports

Check listening ports

ss -tuln

Common ports

22 → SSH
80 → HTTP
443 → HTTPS
3306 → MySQL

## Port Concept

Example

192.168.1.10:3000

192.168.1.10 → machine IP
3000 → application port

## Network Scanning

Find devices in network

nmap -sn 192.168.1.0/24

## Check Local Devices

ip neigh

## DNS

Check DNS resolver

cat /etc/resolv.conf

Example

127.0.0.53

## Public IP

curl ifconfig.me