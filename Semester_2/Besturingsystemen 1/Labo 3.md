
# Besturingssystemen 1 (MBI10a) - Labo 3

Dit kan worden gebruikt voor Labo 3 van besturingssystemen.
> Belangrijk! Labo 1 en 2 moeten volledig afgerond zijn om aan dit labo te kunnen beginnen.

## README
Deze documentatie is gebaseerd op het labo dat je [hier](https://github.com/swenr/operating-systems/tree/master/Storage%2C%20Shares%20en%20rechten) kan terugvinden.
Sommige teksten zijn gekopieerd.
Er kunnen geen rechten worden ontleend of aansprakelijkheid worden aanvaard.

# Voorbereiding
Voeg aan je Windows Server een extra schijf toe. Dit doe je via VMWare, onder instellingen van de VM.
> Om de schijf te kunnen toevoegen moet je VM wel uit staan!

Als je de schijf hebt toegevoegd, start je de Windows Server weer op.
Je gaat naar Computer Management -> Disk Management.
Je zou dan onderstaan beeld moeten zien.
> Screenshot toevoegen

Er staat nu dat disk 1 offline is, maar we willen hem natuurlijk activeren en kunnen gebruiken.
- Je klikt met je **rechter** muisknop op de disk en klikt op **Online**, zodat deze geactiveerd wordt.

Er staat nu Not Initialized
- Je klikt met je **rechter** muisknop op de disk en klik nu op Initialize Disk, kies verder voor GPT.

> Screenshot toevoegen

Daarna moeten we nog een volume toevoegen aan de schijf zodat deze bruikbaar is.
- Klik in de **Unallocated** space met je **rechter** muisknop en klik op **New Simple Volume...**.
> Screenshot toevoegen
- Je laat alle standaard waarden staan maar past wel het volgende toe:
   - Drive-letter: M
   - Filesystem: NTFS
   - Label: ShareDisk

# Sharing
 Nu moet de disk gedeeld worden met andere gebruikers op de computer.
 - Open Verkenner
 - Rechter muisknop op de ShareDisk
 - Open het tab Sharing
 - Ga naar Advanced Sharing
 - Vink Share This Folder aan
 - Geef het de naam NetShare
 - Sluit het venster
 - Maak nu een txt bestandje in de schijf om te testen.

Ga naar je Windows client en zoek de share in verkenner en bekijk het bestand.
Kan je het bestand bekijken, bewerken, verwijderen?
> Dit kan je niet, de client heeft enkel lees rechten.

De lector raad aan om volgende [filmpje](https://www.youtube.com/watch?v=GfmkD12ywfw) te bekijken en [deze blog post](https://blog.netwrix.com/2018/05/03/differences-between-share-and-ntfs-permissions/) te lezen en zelf ook dingen ervan uit te voeren.
Zelf raad ik aan [dit filmpje](https://www.youtube.com/watch?v=fJHFmt6F0Rc&list=PLJcaPjxegjBVnEN8c6O8w1mNit4WGeAWN&index=14&t=0s) te bekijken, hierin wordt alles heel duidelijk uitgelegd en met een exacte demo.

## In de praktijk
Om verder te kunnen gaan met het labo moeten we sharing opnieuw uitschakelen op de omgekeerde manier als we het hebben ingeschakeld.

- Ga je naar `Server Manager` en 
- Ga naar `File and Storage Server`
- Selecteer `Shares`
- Je zou dan volgende scherm moeten zien
> Screenshot toevoegen

- Verwijder het tekstbestand uit de share via verkenner
- maak volgende makken aan
  - SalesShare
  - HRShare
  - EngeneeringShare
- Ga terug naar `Server Manager` ( het scherm in de bovenstaande screenshot)
- Onder `Tasks` kiezen we voor `nieuwe Share`
- We maken een `SMB Share - Quick aan`.
- Geef het pad op van de SalesShare folder en geef de share een naam
- Bij `Permissions` kies je voor `Customize permissions`
- `Disable Inheritance`
- Voeg de groep Sales toe en geef hen `Full Control` rechten
- Je ziet dan volgend eindresultaat
> Screenshot toevoegen

- Doorloop de wizard verder.
- Log nu in op de Windows client met een Sales gebruiker om te kijken als je aan de share kan en alle rechten hebt

## Shared folders in Active Directory
- Open `Active Directory Users and Computers`
- Klik op `Action` -> `new` -> `Shared folder`
- Geef de naam op en het pad van SalesShare
- Open `properties` en voeg het keyword `financial` toe 
- Ga daarna naar je Windows client en zoek naar `financial` op onderstaande locatie
> Screenshot toevoegen

# Referentie (lezen ter info)
### NTFS-permissies voor folders

Voor een folder op een NTFS-permissie kunnen groepen (of eventueel individuele accounts) volgende (standaard)-permissies krijgen:

-   List folder contents. Wie op folder F deze permissie heeft, kan de inhoud van F (lijst van bestanden en subfolders) lezen.
    
-   Read. Wie op folder F deze permissie heeft, kan:
    
    -   de inhoud van F lezen, zoals bij de vorige permissie,
        
    -   de inhoud van bestanden en subfolders van F lezen,
        
    -   attributen, permissies en eigendomsrechten van F lezen.
        
    
-   Read & execute. Wie op folder F deze permissie heeft, heeft de readpermissie maar bovendien ook de zgn. traverse-permissie. Dit is nuttig in volgende situatie: een folderstructuur: …​\dir1\F. Wie geen permissie heeft op dir1 en "read & execute"-permissie heeft op F kan niet bladeren via verkenner en zo naar F gaan maar het kan wel door de volledige padnaam op te geven.
    
-   Write. Wie op folder F deze permissie heeft, kan:
    
    -   in F bestanden en subfolders creëren,
        
    -   in F bestanden en subfolders verwijderen,
        
    -   de attributen van F wijzigen,
        
    -   de permissies en de eigendomsrechten van F lezen maar niet wijzigen.
        
    
-   Modify. Wie op folder F deze permissie heeft, kan:
    
    -   alles wat iemand met de "read & execute"-permissie kan,
        
    -   alles wat iemand met de "write"-permissie kan,
        
    -   F ook verwijderen.
        
    
-   Full control. Wie op folder F deze permissie heeft, kan:
    
    -   alles wat iemand met de "modify"-permissie kan,
        
    -   de permissies en de eigendomsrechten van F en zijn subfolders en bestanden wijzigen.
        
    

### NTFS-permissies voor bestanden

De zopas opgesomde permissies kunnen ook toegekend worden voor individuele bestanden. Sommige hebben uiteraard een enigszins andere betekenis. * Read. Wie op bestand B deze permissie heeft, kan:  **de inhoud van B,** attributen, permissies en eigendomsrechten van B lezen. * Read & execute. Wie op bestand B deze permissie heeft, kan:  **alles wat iemand met de "read"-permissie kan,** B ook laten uitvoeren (als B een uitvoerbaar bestand is). * Write. Wie op bestand B deze permissie heeft, kan:  **B wijzigen,** de attributen van B wijzigen,  **de permissies en de eigendomsrechten van B lezen maar niet wijzigen. * Modify. Wie op bestand B deze permissie heeft, kan:** alles wat iemand met de "read & execute"-permissie kan,  **alles wat iemand met de "write"-permissie kan,** B bovendien ook verwijderen. * Full control. Wie op bestand B deze permissie heeft, kan:  **alles wat iemand met de "modify"-permissie kan,** de permissies en de eigendomsrechten van B wijzigen.

#### Toepassing van NTFS-permissies

Voor elk van deze permissies kan de instelling toegekend (allow) of geweigerd (deny) zijn, of geen van beide. Een account kan in meerdere groepen zitten, waarbij de verschillende groepen andere rechten toekennen aan een bepaald object (map, file). Als men als lid van één groep permissie heeft, dan krijgt de gebruiker toegang, tenzij er ergens anders "geweigerd" staat. Als men behoort tot een groep waarvoor een permissie geweigerd is, heeft men die permissie niet, ongeacht welke de permissies zijn van andere groepen waarvan men ook deel uitmaakt. Een folder erft de permissies van de bovenliggende folder, d.w.z.: als iemand een permissie heeft op een folder dan heeft hij die in principe ook op een subfolder. Men kan dit overerven echter wel blokkeren.

NTFS-permissie zijn van toepassing als een gebruiker lokaal (= aan de computer zelf) werkt, maar ook als hij over het netwerk (bijv. met een gedeelde map) werkt. Andere bestandssystemen, zoals FAT32 en exFAT ondersteunen het concept van permissies niet; daar hebben alle gebruikers toegang tot alle bestanden. Het toekennen van NTFS-permissies gaat via Windows Verkenner door te rechterklikken op de map of het bestand en te gaan naar Properties, Security.

Onafhankelijk van de share-permissies zijn de NTFS-permissies altijd van toepassing (dus onafhankelijk of het object via het netwerk of lokaal gebruikt wordt). Voor netwerkobjecten gelden dus zowel de share- als NTFS-permissies. De meest restrictieve permissie is de eigenlijke permissie.

### Gebruikers en gebruikersgroepen (AGDLP)

Gebruikersbeheer is wellicht de meest complexe taak van een netwerkbeheerder. Zoals we hierboven gezien hebben, wordt toegang tot bestanden en andere bronnen geregeld via permissies.

Het is onverstandig permissies te geven aan individuele gebruikers. In plaats daarvan worden  **globale groepen**  gecreëerd. Gebruikers worden dan ondergebracht in globale groepen (een gebruiker kan tot meerdere groepen behoren). De term  **globaal**  verwijst ernaar dat de groep op het ganse domein bestaat. Sinds Windows 2000 bestaan er ook universele groepen. Dit type groep is nuttig wanneer meerdere domeinen via een netwerk verbonden zijn en als gebruikers van het ene domein toegang moeten hebben tot hulpbronnen van het andere domein. lees volgende  [tekst](https://ss64.com/nt/syntax-groups.html).

Permissies worden toegekend aan domein-gebonden groepen (E. domain local). De beheerder kan individuele gebruikers of globale groepen toekennen aan zo een domein-gebonden groep.
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTE3MDAwMjU2LDExMzY0MjE1OTIsMTQ1Mj
k5ODQ4OCwtMjA5NzQ2NTQyLDk5NjE4NjQzNV19
-->
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMTc4NDg1MDJdfQ==
-->