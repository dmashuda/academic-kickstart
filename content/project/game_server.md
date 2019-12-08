---
title: "Game Server"
date: "2016-01-01"
description: "A real time multiplayer game server"
tags:
  - "go"
  - "concurrency"
  - "udp"
  - "networking"
  - "game"
#titlecolor: "#ffab40" #ffab40
---

Car combat was designed and built for CS481(Senior Software Project). Car combat
is a real-time multiplayer game. Car combat uses an architecture with
an authoritative server. Each client connects to the server and communicates over
a UDP socket. Each client streams commands to the server, and the server broadcasts
the current State of the Game to all of the connected clients. The commands and
GameState are described below:
![alt text](https://raw.githubusercontent.com/awesomegroupidunno/senior-design/master/shared.png)

The game server runs its udp receiver on 2 goroutines, one for sending GameStates
 and one for receiving game commands. The main game loop in the GameManager
 is run on its own goroutine. Each Game command has a corresponding Command
 Processor which mutates the GameState for its corresponding command.

![alt text](https://raw.githubusercontent.com/awesomegroupidunno/senior-design/master/server.png)

### Project Information
###### Project Contributers:
 - [Daniel Mashuda](http://danmashuda.com/about)
 - Austin Decker
 - Austin Forry

###### Install dependencies:
```
    go get .    
```


###### Run Unit Tests:
```
    go test -v ./...  
```


###### Run Server:
```
    go run server.go  
```


By default, the server listens on port: 10001, this can be configured in the server.go file
Car combat client implementation is located:  [here](https://github.com/awesomegroupidunno/game-client)