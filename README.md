# config

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/c1930d244a884c23b4b2bedd4367a400)](https://www.codacy.com/app/avidnet/config?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Avidnet/config&amp;utm_campaign=Badge_Grade)

## Inroduction
Useful configurations about Avidnet infrastructure and platform.

## Server
These servers are from Avidnet IT unit. Each of these servers may have available ssh from outside.

| Hostname       | IP            | Outside Port |
|:-------------- |:-------------:|:------------:|
| parham-usvm-2  | 192.168.73.3  | 3032         |
| mongo-usvm-1   | 192.168.73.2  |              |

These servers are virtualized on a Hardware node.

| Hostname | IP            |
|:---------|:-------------:|
| node-1   | 192.168.73.5  |

- Current Public IP Address: 178.131.34.210

## Remote Access
To have better security, Avident has a minimum number of open ports.
For having access to a local host, you can use ssh local port forwarding.

```sh
# maps port 8080 of the 127.0.0.1 to port 80 of the 192.168.73.254 in the avidnet from parham-usvm-2
ssh -L 8080:192.168.73.254:80 178.131.34.210 -p 3032
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
