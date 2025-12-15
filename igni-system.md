# The Igni System

December 2025

## Introduction

The Igni system is a fully 3D user environment that integrates neatly into any unix-like system. This document details the overarching structure of the Igni system. 

## Socket Directory

Many separate programs play a role in the Igni system. Often, these programs need to communicate with each other.

The Igni system manages many sockets, so it's best to organise them all into directories and sub-directories. 

```
igni/
    cursor/
        lpress
        lrelease
        rpress
        rrelease
    display
```

### `igni/cursor/*`

The `igni/cursor/` directory has 4 sockets that correspond to various mouse cursor events. All sockets in this directory forward incoming data to all connected clients, through the help of [a simple program](https://github.com/igni-project/udscast).

Cursor events are encoded as [CQP](https://github.com/igni-project/cqp) collision queries. Clients can use the collision queries from cursor sockets to determine whether or not a cursor is interacting with a specific area.

The 4 sockets in `igni/cursor/` are:

- `lpress`: Left mouse button pushed down
- `lrelease`: Left mouse button let go
- `rpress`: Right mouse button pushed down
- `rrelease`: Right mouse button let go

### `igni/display`

This socket is managed by a render engine such as [TVrender](https://github.com/igni-project/tvrender).

## Environment Variables

### `$IGNI_SOCKETS`
By default, this environment variable is set to `/run/user/$UID/igni/`. With a UID of 1000, the value of this variable would be `/run/user/1000/igni/`.

