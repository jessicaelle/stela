<p align="center">
<a href="https://docs.forestgiant.com/#stela" target="_blank"><img src="https://dl.dropboxusercontent.com/s/rtqinu44giaelja/Stela-Logo-Horz-Grey.svg?dl=0" height="150" alt="Stela logo"/></a>
</p>

<p align="center">
<a href="https://docs.forestgiant.com/stela/api/" target="_blank"><img src="https://img.shields.io/badge/docs-stela%20api-3DB55B.svg" height="25" alt="Stela API Docs"/></a>   <a href="https://gitter.im/forestgiant/Lobby" target="_blank"><img src="https://img.shields.io/badge/chat-gitter-E1463D.svg" height="25" alt="Forest Giant on Gitter"/></a>
</p>

Stela is a microservice used for discovery of services with gRPC. It uses IPv6 multicast to allow for scalable, distributed discovery on premises.  The project is named after the [stone monuments](https://en.wikipedia.org/wiki/Stela) of the same name.

### Features
* **Distributed**: run one or many Stela instances on any number of computers. 
* **Subscriptions**: subscribe to service names to receive a stream of any services registered or deregistered with that name.
* **Simple**: Stela is meant to be started quickly with little configuration. It only focuses on service registration.

## Installation
### Go
* `go get -u github.com/forestgiant/stela/...`

## Running stela nodes
By default communicates over gRPC `:3100` and IPv6 multicast `:31053`. 
Start your first instance:


`stela -cert /path/to/server.crt -key /path/to/server.key -ca /path/to/ca.crt`

If the SSL files you wish to use are stored as `server.crt`, `server.key`, and `ca.crt` in the directory where the command is issued, you can omit the `cert`, `key`, and `ca` parameters. Alternatively you can use the `-insecure` flag if you don't want to use SSL/TLS gRPC.

`stela`

Start two other instances on the same computer.

$ `stela -port 31001`

$ `stela -port 31002`

Or start another instances on a different computer.

$ `stela`

Services registered with any of the instances will be discoverable by all.

## Examples
* stela watchdog: `cmd/stelawd/`
* Membership: `examples/membership/`
* API Example: Refer to `api/example_test.go`

## Usage
```
  -ca string
    	Path to the private key file for the server. (default "ca.crt")
  -cert string
    	Path to the certificate file for the server. (default "server.crt")
  -insecure
    	Disable SSL, allowing unenecrypted communication with this service.
  -key string
    	Path to the private key file for the server. (default "server.key")
  -multicast int
    	Port used to multicast to other stela members. (default 31053)
  -port int
    	Port for stela's gRPC API. (default 31000)
  -serverName string
    	The common name of the server you are connecting to. (default "Stela")
  -status
    	Shows how many stela instances are currently running. *Only works if you are running a local stela instance.
  -version
    	Prints current version
```
