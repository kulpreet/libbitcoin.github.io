---
layout: home
title: Home
nav_order: 0
---

1. TOC
{:toc}

# What is Libbitcoin?

Libbitcoin is a set of cross platform, open source C++ libraries for
building bitcoin applications. The toolkit consists of
[libraries](#libraries), [examples](/examples), tests and
[applications](/applications)

# Libraries

Libbitcoin decouples the various aspects of bitcoin and provides
API access to developers for building their applications.

The list of libraries and an overview of the APIs they provide is
listed below.

## [libbitcoin-system](https://github.com/libbitcoin/libbitcoin-system)

The system libraries provide the common and essential classes and
APIs needed by the other libraries in the libbitcoin stack. These
classes and APIs can also be used to build components for your
applications.
    
1. [Serialized Data, create public keys and addresses](https://github.com/libbitcoin/libbitcoin-system/wiki/Examples-from-Serialised-Data)
1. [Elliptic Curve Operations](https://github.com/libbitcoin/libbitcoin-system/wiki/Examples-from-Elliptic-Curve-Operations)
1. [Addresses and HD Wallets](https://github.com/libbitcoin/libbitcoin-system/wiki/Examples-from-Addresses-and-HD-Wallets)
1. [Build and sign transactions](https://github.com/libbitcoin/libbitcoin-system/wiki/Examples-from-Building-Transactions)
1. [Even P2WPKH and P2WSH](https://github.com/libbitcoin/libbitcoin-system/wiki/Examples-from-Pay-to-Witness-Transactions)
1. Script Verification - Example pending
1. [Script
    Machine](https://github.com/libbitcoin/libbitcoin-system/wiki/Examples-from-Script-Machine)
    The Script Machine listed above enables "stepping through" a
    bitcoin script to help you debug and build your own scripts.
1. [Fork
   Rules](https://github.com/libbitcoin/libbitcoin-system/wiki/Examples-from-Fork-Rules). Libbitcoin
   uses a fork rules that can be passed in to the various API calls to
   change the behaviour of the the API.

## [libbitcoin-network](https://github.com/libbitcoin/libbitcoin-network)

Libbitcoin Network is a partial implementation of the Bitcoin P2P
network protocol. All protocols that require access to a
blockchain are not included here.

[libbitcoin-node](https://github.com/libbitcoin/libbitcoin-node)
library extends the P2P networking capability and incorporates
[libbitcoin-blockchain](https://github.com/libbitcoin/libbitcoin-blockchain)
in order to implement a full node. The
[libbitcoin-explorer](https://github.com/libbitcoin/libbitcoin-explorer)
library uses the P2P networking capability to post transactions to the
P2P network.

## [libbitcoin-database](https://github.com/libbitcoin/libbitcoin-database)

Libbitcoin Database is a custom database build directly on the
operating system's [memory-mapped
file](https://en.wikipedia.org/wiki/Memory-mapped_file) system. All
primary tables and indexes are built on in-memory hash tables,
resulting in constant-time lookups. The database uses [sequence
locking](https://en.wikipedia.org/wiki/Seqlock) to avoid blocking the
writer. This is ideal for a high performance blockchain server as
reads are significantly more frequent than writes and yet writes must
proceed without delay. The
[libbitcoin-blockchain](https://github.com/libbitcoin/libbitcoin-blockchain)
library uses the database as its blockchain store.


## [libbitcoin-blockchain](https://github.com/libbitcoin/libbitcoin-blockchain)

Libbitcoin Blockchain implements protocols for header, block, and
transaction validation, storing these and reorganising the blockchain
as needed. 

The libbitcoin-blockchain uses libbitcoin-network to request data as
needed, and libbitcoin-database to store and read the required
data. libbitcoin-blockchain assumes that libbitcoin-database is
provides constant time read and write operations.

The transaction validation in blockchain is broken down into those
that require 1) chain and transaction state and 2) checks that require
chain state, block state and perform script metadata.

## [libbitcoin-consensus](https://github.com/libbitcoin/libbitcoin-consensus)

This library includes the following 35 files considered to be bitcoin
script consensus-critical (in bitcoin core). These files are identical
to those used in version 0.19.0 of bitcoin core.

Libbitcoin natively implements consensus checks that are redundant
with
[libbitcoin-consensus](https://github.com/libbitcoin/libbitcoin-consensus). Libbitcoin
includes a full bitcoin client and server SDK. This includes the full
node implementation
[libbitcoin-node](https://github.com/libbitcoin/libbitcoin-node),
which builds on [libbitcoin](https://github.com/libbitcoin/libbitcoin)
and
[libbitcoin-blockchain](https://github.com/libbitcoin/libbitcoin-blockchain).

The
[libbitcoin-blockchain](https://github.com/libbitcoin/libbitcoin-blockchain)
configuration provides the `--with-consensus` option. This allows the
developer to select either `libbitcoin` native or
`libbitcoin-consensus` checks. The option defaults to `yes` so that by
default all
[libbitcoin-node](https://github.com/libbitcoin/libbitcoin-node) and
[libbitcoin-server](https://github.com/libbitcoin/libbitcoin-server)
builds use the same consensus checks as a Satoshi node.

## [libbitcoin-node](https://github.com/libbitcoin/libbitcoin-node)

Is an application that provides a Bitcoin full node based on
[libbitcoin-blockchain](https://github.com/libbitcoin/libbitcoin-blockchain).

Detailed documentation is available on [libbitcoin-node
wiki](https://github.com/libbitcoin/libbitcoin-node/wiki)

## [libbitcoin-server](https://github.com/libbitcoin/libbitcoin-server)

A full Bitcoin peer-to-peer node, Libbitcoin Server is also a high
performance blockchain query server. It can be built as a single
portable executable for Linux, macOS or Windows and is available for
download as a signed single executable for each. It is trivial to
deploy, just run the single process and allow it about two days to
synchronize the Bitcoin blockchain.

Libbitcoin Server exposes a custom query TCP API built based on the
[ZeroMQ](http://zeromq.org) networking stack. It supports server, and
optionally client, identity certificates and wire encryption via
[CurveZMQ](http://curvezmq.org) and the [Sodium](http://libsodium.org)
cryptographic library.

The API is backward compatible with its predecessor
[Obelisk](https://github.com/spesmilo/obelisk) and supports simple and
advanced scenarios, including stealth payment queries. The
[libbitcoin-client](https://github.com/libbitcoin/libbitcoin-client)
library provides a calling API for building client applications. The
server is complimented by [libbitcoin-explorer
(BX)](https://github.com/libbitcoin/libbitcoin-explorer), the Bitcoin
command line tool and successor to
[SX](https://github.com/spesmilo/sx).

Detailed documentation is available on [libbitcoin-server
wiki](https://github.com/libbitcoin/libbitcoin-server/wiki)

## [libbitcoin-client](https://github.com/libbitcoin/libbitcoin-client)

Bitcoin Client Query Library that talks to
[libbitcoin-server](https://github.com/libbitcoin/libbitcoin-server)
using [libbitcoin-protocol](https://github.com/libbitcoin/libbitcoin-protocol)

## [libbitcoin-protocol](https://github.com/libbitcoin/libbitcoin-protocol)

Provides the protocol provides client server interaction between
[libbitcoin-client](https://github.com/libbitcoin/libbitcoin-client)
and
libbitcoin-server](https://github.com/libbitcoin/libbitcoin-server).

## [libbitcoin-explorer](https://github.com/libbitcoin/libbitcoin-explorer)

Libbitcoin Explorer, or BX, is a command line tool for working with
Bitcoin. It can be built as a single portable executable for Linux,
macOS or Windows and is available for download as a signed single
executable for each. BX exposes over 80 commands and supports network
communication with
[libbitcoin-server](https://github.com/libbitcoin/libbitcoin-server)
or its predecessor [Obelisk](https://github.com/spesmilo/obelisk), and
the P2P Bitcoin network. BX is well documented and supports simple and
advanced scenarios, including stealth and multisig.

Detailed documentation is available on [libbitcoin-explorer
wiki](https://github.com/libbitcoin/libbitcoin-explorer/wiki)

## [libbitcoin-build](https://github.com/libbitcoin/libbitcoin-build)

This repo is internally used by libbitcoin developers to update build
scripts for the various platforms. As an application developer you
most likely won't need to use this.

## Dependencies

The build dependencies between the various libraries is shown in the
figure below.

![Libbitcoin dependencies](/assets/dependencies.png)
