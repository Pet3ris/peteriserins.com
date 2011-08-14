---
layout: post
title: Introducing jacobian
---

## {{ page.title }}
<time>14.08.2011</time>

We Contract Bridge players have never been blessed with good software.
Chess players have it all: protocols, GUIs, engines. Many of them free. In Bridge,
we have a collection of all-in-one packages, ranging from expensive to unusable. The only
means of communication among them are online bridge servers and a protocol used solely at the
World Computer Bridge Championships that requires programs to talk over TCP/IP.

This is not only a barrier of entry in the computer bridge arena, but also is a missed
opportunity in terms of getting more people involved in the game and increasing the overall
level of play. Just look at how fast the Free Robot Bridge tournaments fill up at BridgeBase
Online and it will be clear that there is significant demand for usable and free bridge robots.

A little while ago [Edgars Sedols](http://sedols.com) and I decided to do something about this.
What we wanted was not a revolution in the computer bridge industry but the simple ability to
set a deal and declare it against two robots. So we created jacobian.

Jacobian is a simple, incomplete, but working protocol for computer bridge programs.
With the host program, you specify a deal, vulnerability, contract and the four players by
specifying their executable programs. The host then leads them trough a game of bridge
(currently, only the play of the hand is implemented). That's it.

The "players" can be anything as long as they adhere to the protocol. A GUI can be a player,
serving as an interface to the protocol for a human player. A robot can be a player in which
case the program will be a wrapper for the robot implementing the jacobian protocol.

We wrote everything in Java due to its popularity and cross-platform support. Ironically,
the current version is Unix only, but we're working on that already. The protocol description and the host program can be located at [jacobian-host](https://github.com/Pet3ris/jacobian-host).
The GUI can be found at [jacobian-GUI](https://github.com/Sedols/jacobian-GUI).
A GiB engine wrapper is at
[jacobian-gib-wrapper](https://github.com/Pet3ris/jacobian-gib-wrapper). You will need your own
GiB engine to play though.

The whole package is really rough around the edges at the moment. To get started with it, if
you're on a Unix computer, you will need to fetch the three `.jar` files first. Put them in the
same folder together with your GiB engine. Rename the GiB engine to `gib.exe` if it's named
`bridge.exe` (we are using the free version for our experiments). You can test-drive a hand by
writing

    $ java -jar jacobian-host.jar 'java -jar jacobian-gib-wrapper.jar' 'java -jar jacobian-gib-wrapper.jar' 'java -jar jacobian-gui.jar' 'java -jar jacobian-gib-wrapper.jar' 3031333123220300123320212213021202022103101101003113 NONE 3NS

We have scratched our itch, we can now play a hand with GiB. But we would be happy to continue
working with the community on this if we see some support and potential. You are absolutely
welcome to contribute and/or implement the protocol for your own applications and make the Bridge
world a little bit more open for everyone.
