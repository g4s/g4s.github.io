---
title: "Installing new KVM host on top of Gentoo"
date: "2022-01-06T11:18:34Z"
draft: true
author: ""
authorTwitter: "g4s3"
cover: ""
tags: ["homelabinabox"]
keywords: ["Gentoo", "KVM"]
series: "homelabinabox"
showFullContent: false
readingTime: true
---

Nachdem ich im letzten Artikel schon ein wenig zu [#homelabinabox](/tags/homelabinabox)
erzählt habe, kommen wir heute zum ersten praktischen Teil der Serie: die Installation
des eigentlichen Hosts. Der Witz an der vorgestellten Installation ist, dass wir das 
gesammte Homelab in eine kompakte Kiste mit KVM Hypervisor packen werden. Unter diesen
Gesichtspunkten wird sich natürlich auch die Installation grob in zwei Teile aufteilen:

  * Teil 1 - Installation des Grundsystems (Gentoo Linux)
  * Teil 2 - Die Vorbereitung als Hypervisor

Über den Einsatz von [Gentoo Linux](https://gentoo.org) lässt sich wie bei jeder 
anderen Distribution streiten. Ich selbst verwende Gentoo ganz gerne in Szenarien
wie diesen, da es sehr einfach ist extrem schlanke Systeme zu bauen. (Viele Sachen,
die moderne Distributionen mitbringen sind hier einfach überflüssig.) Daneben bietet
Gentoo als Sourcecode-Distribution den tollen vorteil, dass wir bei jeder
Softwarekomponenten frei entscheiden können, welche Features wir real benötigen und
welche nicht - dies kann man durchaus auch gleichzeitig als Sicherheitsfeature
ansehen. Dieser Artikel reicht natürlich bei weitem nicht eine gute und umfassende
Einführung in Gentoo zu liefern - dennoch werde ich versuchen an allen Stellen 
