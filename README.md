# SIA node server

Allows you to log AJAX Security Systems events and other types of SIA-DC-09 events to…

- an MSSQL database

## Standard compatibility

Currently the option to configure this server as UDP is not implemented, it only receives non-encrypted TCP connections.

This server act as Central Station Receivers (CSR). Encryption support is mandatory for CSRs. So, this is a non-standard project at this time.

## Standard

## Install

```bash
git clone https://github.com/nhereveri/SIAbroker.git
cd SIAbroker
npm i
node server.js --help
```

## Sample config

```yaml
server:
  port: 65000
  diff:
    negative: -20
    positive: 40
dispatcher:
  -
    type: 'mssql'
    format: 'human'
    user: 'foo'
    password: 'P4$$w0Rd'
    database: 'sia-events-db'
    server: '10.0.2.15'
    port: 1433
```

## Execution

```bash
# default config (from config.yml)
node server.js

# specify service port
node server.js --port 65000

# debug messages to console
node server.js --debug
```

## Dispatchers

At the moment it only supports dispatchers type ...

- `mssql`

You can specify the number of dispatchers you need.

```yaml
dispatcher:
  -
    type: 'mssql'
    format: 'human'
    user: 'user'
    password: '$3cr3t'
    database: 'sia-events'
    server: '127.0.0.1'
    port: 1433
  -
    type: 'mssql'
    format: 'human'
    user: 'other'
    password: '$3cr3t'
    database: 'sia-events-backup'
    server: '190.13.132.109'
    port: 1433
  -
    type: 'console'
    format: 'human'
```

## TODO

- adding other types of distpatchers
- use Facade pattern in dispatch function
- use UDP connections
- decrypt messages
