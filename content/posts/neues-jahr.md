---
title: "Neues Jahr, neuer Blog?"
date: 2022-01-03T13:46:30Z
draft: true
tags: 'homelabinabox'
---
Ja, ja immer wieder irgendwie das leidige Thema: viele Menschen wollen
immer unbedingt "Vorsätze" fürs neue Jahr setzen. Persönliche Meinung - 
eher ein wenig Schwachfug. Ich sete mir da lieber neue Projekte, die
ich im neuen Jahr absolvieren möchte. Natürlich steht dieses Projekt
bereits fest für das Jahr 2022. Die Idee dazu kam mir zwischen den Jahren.

Also noch einmal kurz Hardware eingekauft und schon mal grob mit der Planung
zwischen Raclette, Rotwein und Gänsekeule begonnen. So schnell war
[#homelabinabox](/tags/homelabinabox) geboren. Die nächsten Wochen und
Monate sind also verplant, sofern jetzt nix mehr dazwischen kommt.

Aber worum geht des eigentlich dabei? Um etwas ganz einfaches... ok
für einige unter Euch vielleicht auch nicht so einfach -  das ist ok, 
ehrlich! Hier muss niemand hardcore Linux oder Unix Crack sein. Das ist
wirklich nicht nötig. Aber zurück zum Thema: wer sich ein klein wenig
mit Linux, DIY und Computing stößt, trifft immer mal wieder gerne auf
kleine SBCs (Single Board Computer) wie den Raspberry Pi. Diese Boards
sind grandios und haben vielen Menschen den Zugang zu Linux eröffnet - 
ich bin wirklich ein Fan von SBCs.
Allerdings wunder ich mich manchmal doch sehr darüber, wie manch einer
mit genau diesen Boards umgeht: Da werden Mailserver oder NAS mit den
kleinen Boards betrieben. (Und natürlich noch vieles andere.) Manch
einer hat bei sich zu Hause ein kleines Batallion stehen um sein sog.
"Homelab" zu realisieren. Als Begründung kommt dann oftmals, das die Boards
gut verfügbar, sowie günstig wäre, aber auch das sich die Stromkosten in
Grenzen halten würden.
NUn gut, das kann man so sehen.... ich bevorzuge dennoch eine klassische
x86 Architektur und wenn ich ehrlich bin, finde ich es auch nicht so
spannende eine Armada von Boards rumliegen zu haben um alltägliche Services
zu relalisieren: dies waren übrigens auch einige der Gründe, wie ich zu
#HomelabInABox kam. Der Gedanke ist ganz einfach, denn wir nehmen eine
Maschine auf x86-Basis mit halbwegs potenter Hardware und werden darafu
uns er Homelab in den nächsten Wochen und Monaten aufbauen.

Ich werde versuchen Euch in verständlicher Sprache und mit den nötigen
Hintergrundinformationen angereichert zu zeigen, wie man ein gesammtes
Homelab aufbauen und betreiben kann. Da drunter wird es auch Schmankerl geben
wie den Aufbau einer Nextcloud-Instanz aber auch auch einen 
(Linux-)Terminalserver.

## die Platform
Sicher seit Ihr schon gespannt, was hier als Hardware jetzt eingesetzt wird,
vorab gibt es aber noch ein paar Informationen, die auch alle folgenden
Artikel betreffen werden:

  * Strom und Traffic sind mir relativ egal in dem Szenario, da die Kiste
    in einem Rechenzentrum steht und die Tarife weder mit privaten noch
    mit dem was man daheim bekommt vergleichbar ist.

  * Der Server hat eine fixe public IPv4 - deswegen werde ich mir hier
    alles sparen was an privaten Hausanschlüssen interesant sein kann wie
    DDNS(DynDNS), Zwangsdisconect, IPv4 only Stack, DSL lite....

  * Domains laufen über einen unabhängigen Registrar (der die Domains auch
    via API verwalten kann: ja, hier könnte man sein eigenens DDNS bauen)

  * Ich selbst wähle Software, die mir gut passt - wem es nicht schmeckt, kann
    gerne etwas anderes verwenden, das ist ok, bedeutet aber auch, das man dann
    schauen muss, wie das ins Gesamtkonzept passt.

Nun aber doch mal zu der Hardware, die ich günstig zwischen den Jahren als
Posten auf der Serverbörse eines deutschen RZ Betreibers und Hosters 
einkaufen konnte:

  * [Intel Core i7-3930](https://ark.intel.com/content/www/de/de/ark/products/63697/intel-core-i73930k-processor-12m-cache-up-to-3-80-ghz.html)
  * 1 x 1GB Intel Uplink symmetrisch ans Backbone 
  * 2 x 6 TB SATA Storage
  * 65,54 GB DDR3 RAM ( 8 x 8192 MB non ECC )
  * OS: rescue console

Auf den ersten Blick erkennt man gleich, dass wir hier eher keine Storage Box
vor uns stehen haben (was auch auch wirklich nicht schlimm ist), sondern dieser
Server in seinem früheren Leben sicherlich einmal als Applikation-Server
seinen Dienst tun durfte. Natürlich gibt es immer bessere Hardware..., aber
für unsere Belange wird diese ersteinmal reichen. So würden uns theoretisch
5 (exklusive) vCPUs für virtuelle Maschinen durch den i7-3990 zur verfügung
gestellt werden - wenn man mehr benötigt, kommt man in der i-Sereies generell
bald an die Grenzen. Mehr RAM kann übrigens nicht in die Maschine eingebaut 
werden, mehr kann der 3990 derzeit einfach nicht verarbeiten. Die für uns 
wichtige VT-x Extension unterstützt natürlich der 3930.

Preis-/Leistung war in dem Paket ok und ich fand es ganz apart, dass der Server
nur mit einem Minimal-Linux vorinstalliert geliefert wurde (dies übrigens in
unter 4 Stunden).

## Das Betriebssystem
Ok. Wir haben da jetzt für unser Projekt Metal rumstehen, aber immer noch kein 
wirkliches Betriebssystem. Jedenfalls nichts womit wir gleich anfangen können zu 
arbeiten. Wir könnten jetzt ellenlang darüber diskutieren was es werden soll. (Ich
vermute wir müssen nicht darüber diskutieren, ob es ein Linux wird. Tatsächlich
würde sich das Projekt auch sehr entspannt unter FreeBSD bewerkstelligen lassen.)
Oder wir nehmen einfach eine schlanke Distribution, die ich für Server Dienste und
Container bevorzuge: [Gentoo](https://gentoo.org). Zur Diskussion hätten übrigens
bei mir noch gestanden Arch Linux (DailyDriver auf Benutzer-Endgeräten), SuSe oder
Fedora (die beiden letztgenannten habe ich viel beruflich an der Backe: unsere
Kunden setzen in der Regel Suse Enterprise Linux oder RedHat Enterprise Linux ein).

Sicherlichlich wird diese Wahl einige nicht so richtig glücklich machen, da sie sich
eher etwas Debian-/Ubuntu-based gewünscht hätten. Das ist nicht schlimm und ich
traue erst einmal jedem zu eine Ubuntu-Installation durch zu führen ohne daran zu
scheitern. Für unser Gesamtprojekt wird dies aber auch nicht weiter tragisch sein.

## Ausblick
So weit so gut. Ihr wisst jetzt im Groben um was es geht und was an Hardware zur
Verfügung steht. Im nächsten Artikel werden wir uns der Gentoo und KVM Installation
auf unserer neuen Maschine widmen. Wenn Ihr etwas anderes als Gentoo bevorzugt´
(was auch vollkommen ok ist), so ist das kein Beinbruch: in Zukunft werden wir
eher standardisierte Wege nutzen um die benötigten virtuellen Maschinen auf die
Hardware zu bringen. Spricht wir werden libvirt verwenden. Es ist dann unerheblich
auf welcher Distri KVM läuft. Ich kann dennoch jedem einmal raten den nächsen Artikel
zu folgen und auch einmal einen Blick in das Gentoo-Handbook zu werden. Beides ist
sicherlich vom Informationswert für jeden Linux Nutzer nicht ganz verschwendete
Lebenszeit. Was ich mir von Euch wünschen würde: seit positiv gegenüber Dokumentation
eingestellt und schaut auch einmal über den eigenen Tellerrand.

Bis demnächst dann.
