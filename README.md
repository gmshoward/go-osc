# GoOSC

![Build](https://github.com/gmshoward/go-osc/actions/workflows/test.yml/badge.svg) [![GoDoc](https://godoc.org/github.com/gmshoward/go-osc/osc?status.svg)](https://godoc.org/github.com/gmshoward/go-osc/osc) [![Coverage Status](https://coveralls.io/repos/github/gmshoward/go-osc/badge.svg?branch=master)](https://coveralls.io/github/gmshoward/go-osc?branch=master)
[![Go Report Card](https://goreportcard.com/badge/github.com/gmshoward/go-osc)](https://goreportcard.com/report/github.com/gmshoward/go-osc)

This is a fork of hypebeast's [Open Sound Control (OSC)](http://opensoundcontrol.org) [library for Golang](https://pkg.go.dev/github.com/hypebeast/go-osc/osc). Its only deviation from the original is to provide an interface for showing what port was *actually chosen* when the listener was started.

## Features

-   OSC Bundles, including timetags
-   OSC Messages
-   OSC Client
-   OSC Server
-   Supports the following OSC argument types:
    -   'i' (Int32)
    -   'f' (Float32)
    -   's' (string)
    -   'b' (blob / binary data)
    -   'h' (Int64)
    -   't' (OSC timetag)
    -   'd' (Double/int64)
    -   'T' (True)
    -   'F' (False)
    -   'N' (Nil)
-   Support for OSC address pattern including '\*', '?', '{,}' and '[]' wildcards

## Install

```shell
go get github.com/hypebeast/go-osc
```

## Usage

### Client

```go
import "github.com/hypebeast/go-osc/osc"

func main() {
    client := osc.NewClient("localhost", 8765)
    msg := osc.NewMessage("/osc/address")
    msg.Append(int32(111))
    msg.Append(true)
    msg.Append("hello")
    client.Send(msg)
}
```

### Server

```go
package main

import "github.com/hypebeast/go-osc/osc"

func main() {
    addr := "127.0.0.1:8765"
    d := osc.NewStandardDispatcher()
    d.AddMsgHandler("/message/address", func(msg *osc.Message) {
        osc.PrintMessage(msg)
    })

    server := &osc.Server{
        Addr: addr,
        Dispatcher:d,
    }
    server.ListenAndServe()
}
```

## Tests

```shell
make test
```
