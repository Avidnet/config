# config

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/c1930d244a884c23b4b2bedd4367a400)](https://www.codacy.com/app/avidnet/config?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Avidnet/config&amp;utm_campaign=Badge_Grade)

## Inroduction
Useful configurations about Avidnet infrastructure and platform.
To support `https` we use [Certbot](https://certbot.eff.org/docs/using.html#manual) with Nginx and Ubuntu 18.04.
Please note that we use dns plugin of certbot. Avidnet monitoring is based on [uptime robot](https://uptimerobot.com).
Avidnet has a gateway for its lora communications that use [TTN](http://thethingsnetwork.org) as its Network Server.

## Server
These servers are from Avidnet IT unit. Each of these servers may have available ssh from outside.

| Hostname       | IP            | Outside Port |
|:-------------- |:-------------:|:------------:|
| avid-nginx     | 192.168.73.1  |              |
| parham-usvm-2  | 192.168.73.3  | 3032         |
| mongo-usvm-1   | 192.168.73.2  |              |
| taha-usvm-1    | 192.168.73.4  | 3031         |
| rhf2s008       | 192.168.73.10 |              |

These servers are virtualized on a Hardware node.

| Hostname | IP            |
|:---------|:-------------:|
| node-1   | 192.168.73.5  |

- Current Public IP Address: 178.131.34.210 (which is maped to `platform.avidnet.io`).

## Remote Access
To have better security, Avident has a minimum number of open ports.
For having access to a local host, you can use ssh local port forwarding.

```sh
# maps port 8080 of the 127.0.0.1 to port 80 of the 192.168.73.254 in the avidnet from parham-usvm-2
ssh -fNT -L 8080:192.168.73.254:80 178.131.34.210 -p 3032
```
```
  -L    Local port forwarding
  -f    Requests ssh to go to background just before command execution.
  -N    Do not execute a remote command.
  -T    Disable pseudo-tty allocation.
```

> Use local port forwarding to forward data securely from an application client running on the same computer as the Secure Shell client.

```
ssh -L listening_port:app_host:hostport user@sshserver
```

## MongoDB
In avidnet we have replicated mongo databases. So in this environment our db_urls as the following:

```sh
mongodb://127.0.0.1:27017,192.168.73.2:27017.192.168.73.2:27018/?replicaSet=avidnet
```

To mintor our database inferastructure we use `mongostat` and `mongotop` from [mongo-tools](https://github.com/mongodb/mongo-tools).

## Monitoring
In avidnet we monitor following component of I1820, our open source IoT Platform:

- Physical node (Load and FreeMem)
- Link component
- Vernemq broker
