---
title: "Go-Imgur"
date: "2016-02-01"
description: "A basic imgur api client for go"
tags:
  - "go"
  - "imgur"
  - "api"
  - "golang"
#titlecolor: "#ffab40" #ffab40
---

A basic api client for [imgur](https://api.imgur.com/). Currently I have only implemented the features of the imgur api that I use for other projects.

If you would like another piece of functionality implemented, open an [issue](https://github.com/dmashuda/go-imgur/issues/new) or implement it yourself and submit a pull request

## Installation:
```
    go get github.com/dmashuda/go-imgur     
```


## Example Usage:
#### Creating a Client:
```
    client := imgur.NewClient(clientID)   
```
*clientID is issued by imgur on a per application basis*

#### Retrieving album information:
```
    aww, err := client.GetAlbum("/gallery/r/CorgiGifs", 0, 20)    
```