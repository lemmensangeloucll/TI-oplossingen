# Besturingssystemen 1 (MBI10a) - Linux
Dit kan worden gebruikt voor Linux van besturingssystemen.
## README
Deze documentatie is gebaseerd op het labo dat je [hier](https://github.com/swenr/operating-systems) kan terugvinden. Sommige teksten zijn gekopieerd. Er kunnen geen rechten worden ontleend of aansprakelijkheid worden aanvaard.

## Virtualisatie
Door middel van virtualisatiesoftware  zoals VMware, kunnen diverse besturingssystemen (zoals Linux, FreeBSD, Windows, ... ) en  applicaties in een  virtuele machine gedraaid  worden.

De computer die de verschillende  virtuele machines host of draait, wordt  host  genoemd.

De virtuele machines zelf  worden  guests  genoemd. De virtuele machines worden op de harde  schijf van de host opgeslagen in typisch twee tot 10 bestanden.

Om zo optimaal  mogelijk  gebruik  te  maken van virtuele machines op je host (computer), dient support hiervoor  geactiveerd  te  worden.

>Indien je een error krijgt, zet Intel-VT of AMD-V aan in je systeem BIOS

## Software
Je kan gebruik maken van VMWare of VirtualBox.
>VMWare kan je terug [hier](https://webfiles.ucll.be/)  terugvinden.
>Volg Education -> CourseInfo -> Mana&Tech -> Toeg. Info -> Comp.Netw1 ->VMware

### Linux ISO
Je kan de Debian ISO [hier](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/) downloaden.
Kies voor het bestand dat eindigt op `-amd64-netinst.iso`

## SHELL
Een shell is de interpreter die commando's vertaalt die door een gebruiker zijn ingevoerd in acties die door het besturingssysteem moeten worden uitgevoerd. Commando's worden bij de prompt ingevoerd.
>user@system:/home/user>

`shell => bash, tcsh, zsh, ...`

Een CLI is uitdagend als je hier nog geen ervaring mee hebt.

 **Commando’s en hun opties moet je (in het begin) van buiten leren!**
 
## Syntax Shel
`[root@linux ~]# command [options] [arguments]`
**OPTIONS**
are used  to  modify  the  core  behaviour of the  command
**ARGUMENTS**
are used  to  provide  additional information such as a file name or a user name to  the  command

## Commando's
Probeer volgende commando's eens uit in de terminal:
- `cal 1 2015`
- `cal 4 2016`
- `cal 1 1`
- `history`
- `pwd`
- `cd`
- `ls`
- `cp`
- `touch`
- `rm`
- `rmdir`
- `cat`
- `grep`
- `find`
- `tree`
> Bekijk zeker ook de cheat sheets die Rudi geeft.
## NANO
Nano is een manier om
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyOTYzOTgzN119
-->