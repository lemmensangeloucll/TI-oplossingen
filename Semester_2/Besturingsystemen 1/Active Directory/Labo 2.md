

# Besturingssystemen 1 (MBI10a) - Labo 2

Dit kan worden gebruikt voor Labo 2 van besturingssystemen.
> Belangrijk! Labo 1 moet volledig afgerond zijn om aan dit labo te kunnen beginnen.

## README
Deze documentatie is gebaseerd op het labo dat je [hier](https://github.com/swenr/operating-systems/tree/master/OU's%20en%20groepsbeleid) kan terugvinden.
Sommige teksten zijn gekopieerd.
Er kunnen geen rechten worden ontleend of aansprakelijkheid worden aanvaard.

# GPO
GPO staat voor **Group Policy Object**.
Indien je niet volledig begrijpt wat GPO betekent en wat het voor je kan doen kan je een van de volgende filmpjes bekijken:
[Video 1](https://www.youtube.com/watch?v=azup50LaIN0)
[Video 2](https://www.youtube.com/watch?v=KSTKGChQus0&list=PLJcaPjxegjBVnEN8c6O8w1mNit4WGeAWN&index=14)


Open op je Windows server **Group Policy Management**.

- Met de rechtermuisknop klik je op `cosci.be`
- Klik daarna op `Create a GPO in this domain, and Link it here...`
- Je geeft het de volgende naam: `Enforce Password Policy`
- Klik nu met je **rechter** muisknop op de nieuwe GPO dat werd aangemaakt
- Klik dan op `edit`
- In het linker venster doe je het volgende
  - Klik `Computer Configuration` open
  - Klik `Policies` open
  - Klik `Windows Settings` open
  - Klik `Security Settings` open
  - Klik `Account Policy` open
  - Klik nu op `Password Policy`
 -  Dubbelklik op `Password must meet complexity requirements`
     - Klik `Define this policy setting` aan
     - Klik op `Enabled`
     - Klik op `Apply`
     - Klik op `OK`

Zorg nu dat de laatste 10 wachtwoorden worden onthouden, een wachtwoord minstens 1 dag oud moet zijn voor het veranderd kan worden, na een jaar veranderd moet worden, het minstens 8 tekens heeft en dat het niet opgeslagen wordt met een terugkeerbare encryptie.

> Probeer dit eerst zelf, hieronder vindt je de stappen moest het niet lukken.

 -  Dubbelklik op `Enforce password history`
     - Klik `Define this policy setting` aan
     - Vul hier `10` in
     - Klik op `Apply`
     - Klik op `OK`

 -  Dubbelklik op `Minimum password age`
     - Klik `Define this policy setting` aan
     - Vul hier `1` in
     - Klik op `Apply` (je krijgt nu een popup venster)
     - Klik op `OK`
     - Klik op `OK`

 -  Dubbelklik op `Maximum password age`
     - Klik `Define this policy setting` aan
     - Vul hier `365` in
     - Klik op `Apply`
     - Klik op `OK`

 -  Dubbelklik op `Minimum password length`
     - Klik `Define this policy setting` aan
     - Vul hier `8` in
     - Klik op `Apply`
     - Klik op `OK`

 -  Dubbelklik op `Store passwords using reversible encryption`
     - Klik `Define this policy setting` aan
     - Klik op  `Disabled`
     - Klik op `Apply`
     - Klik op `OK`

- Sluit het venster nu af.

Nu gaan we een nieuwe GPO aanmaken voor de groep Sales. We willen bereiken dat zei een wachtwoordlengte van 10 karakters moeten hebben in plaats van 8.

> Probeer dit eerst zelf alvorens onderstaande oplossing te bekijken!

>Test of dit nu effectief zo is door een nieuwe gebruiker aan te maken in de OU van Sales, in te loggen op je Windows 10 client en het wachtwoord proberen te veranderen.
>! De oplossing hiervan staat onderaan onderstaande oplossing !


- Met de rechtermuisknop klik je op `Sales` (dit vindt je terug onder `Employees`)
- Klik daarna op `Create a GPO in this domain, and Link it here...`
- Je geeft het de volgende naam: `Meer karakters` (eigen keuze)
- Klik nu met je **rechter** muisknop op de nieuwe GPO dat werd aangemaakt
- Klik dan op `edit`
- In het linker venster doe je het volgende
  - Klik `Computer Configuration` open
  - Klik `Policies` open
  - Klik `Windows Settings` open
  - Klik `Security Settings` open
  - Klik `Account Policy` open
  - Klik nu op `Password Policy`
 -  Dubbelklik op `Minimum password length`
     - Klik `Define this policy setting` aan
     - Vul `10` in
     - Klik op `Apply`
     - Klik op `OK`

> Waarschijnlijk is je test die je moest uitvoer gefaald. Maar waarom?

 Dit komt doordat we een Policy hebben gemaakt voor de computer en niet voor de user.
 Je kan dit zien aan het begin we kozen toen voor `Computer Configuration` en niet voor `User Configuration` dit wil zeggen dat de computer dus ook in de groep `Sales` moet zitten alvorens deze instellingen zullen worden doorgevoerd.

Daarnaast is het belangrijk te weten dat indien je kiest voor `Computer Configuration` de computer opnieuw moet opstarten alvorens hij de policy ophaalt.
Wanneer je kiest voor `User Configuration` zal de policy worden opgehaald bij het opnieuw inloggen.

Je kan ook de GPO handmatig updaten door volgend commando in cmd uit te voeren:
```
gpupdate /force
```

>Als meerdere GPO’s na mekaar toegepast worden, dan betekent **niet geconfigureerd** de vorig toegepaste instelling blijft en **uitgeschakeld** wat de vorige instelling ook was, ze wordt nu uitgeschakeld.

## Policies debuggen
Wanneer er iets misloopt met het toepassen van een policy, zijn er tools om te kijken waar het probleem precies zit. Een eerste stap is kijken welke regels er nu toegepast werden. Dit kan je doen door in een console-venster het commando `gpresult /v` in te typen. Dit geeft een lijst van alle policies die toegepast worden op de huidige gebruiker, alsook wat extra informatie. Je kan deze informatie ook wegschrijven als een (overzichtelijker) HTML-bestand door het commando `gpresult /H bestand.html`. Wanneer een policy niet toegepast kan worden, gaat de Group Policy Client een foutmelding wegschrijven in het Windows event log. Je kan deze log bekijken door het programma Event Viewer op te starten en te navigeren naar Windows logs.

### Opdracht
- Ga naar `Group Policy Management`
- Hier ga je in je linker tree naar `Marketing`
- Rechter klik op `Marketing` en klik op `Create a GPO in this domain, and Link it here...`
- De eerste geef je de naam `Disable Command Prompt`
- Rechter klik op de zonet aangemaakte GPO en klik op `Edit...`
- In het linker venster doe je het volgende
  - Klik `User Configuration` open
  - Klik `Policies` open
  - Klik `Administrative Templates` open
  - Klik `System` open
 -  Dubbelklik op `Prevent access to the command prompt`
     - Klik `Enabled` aan
     - Klik op `Apply`
     - Klik op `OK`
- Sluit het venster

- Maak hierna een tweede GPO aan en noem deze `Enable Command Prompt`
- Rechter klik op de zonet aangemaakte GPO en klik op `Edit...`
- In het linker venster doe je het volgende
  - Klik `User Configuration` open
  - Klik `Policies` open
  - Klik `Administrative Templates` open
  - Klik `System` open
 -  Dubbelklik op `Prevent access to the command prompt`
     - Klik `Disabled` aan
     - Klik op `Apply`
     - Klik op `OK`
- Sluit het venster

- In de Group Policy Management klik je op de OU `Marketing`
- Rechts verschijnt er een overzicht het tabblad `Linked Group Policy Objects` is actief

Je ziet hier dat Disable Command Prompt bovenaan staat, dit wil zeggen dat de Policy vooraan zal krijgen op alle Policy's eronder.
Als er dus lager een Policy is die dezelfde property aanspreekt zal deze dus niet worden aangepast maar zal deze de waarde van de hoogste behouden.

- Zorg ervoor dat `Disable Command Prompt` bovenaan staat zodat de toegang tot de Command Pormpt zal worden geweigerd.
- Log in op de windows 10 client met een gebruiker die in de OU van `Marketing` zit.
  - Indien je geen gebruiker hebt in deze OU maak je er een aan.
- Open nu Command Prompt
> Dit zal niet lukken. 
- Meld menu af van je Windows 10 client
- Ga terug naar je Windows Server en plaats nu `Enable Command Prompt` bovenaan.
- Log opnieuw in met de gebruiker die in de OU `Marketing` zit.
- Open opnieuw Command Prompt.
> Nu zal het wel lukken.

## Remote Access
- Log in op de Windows 10 client als de domeinbeheerder.
> Je moet inloggen met Administrator maar aangezien er op de windows 10 client ook een  Administrator account aanwezig is zal deze dus het verkeerde account nemen om in te loggen. We loggen in met het volgende om dit te voorkomen.
- `administrator@cosci.be`
- surf nu naar [deze link](https://www.microsoft.com/en-us/download/details.aspx?id=45520).
> Het is mogelijk dat je met je administrator account de browser niet kan openen, je zal moeten inloggen op een andere gebruiker om bv. Google Chrome of Firefox te installeren voor alle gebruikers zodat ook jou administrator op de internet browser kan. Je kan ook de installatie uitvoeren vanaf een gebruiker die wel op Microsoft Edge kan maar dit is niet getest.
- Open nu `Control Panel`
- Klik op `Programs`
- Klik op `Turn Windows features on or off`
- Activeer RSAT


## Oefeningen
### Beperk toegang tot het configuratiescherm & Command Line
- Open `Group Policy Management`
- Maak een nieuwe GPO aan in `Employees`
- Geef deze een naam bv. `Disable C&C`
- Volg volgende structuur in de linker kolom.
- `User Configuration`-> `Policies`-> `Administrative Templates`-> `Control Panel`
- Dubbel klik nu rechts op `Prohibit access to Control Panel and PC settings`
- Vink Enabled aan
- Klik op Apply
- Klik op OK
-  Volg volgende structuur in de linker kolom.
- `User Configuration`-> `Policies`-> `Administrative Templates`-> `System`
- Dubbel klik nu rechts op `Prevent access to the command prompt`
- Vink Enabled aan
- Klik op Apply
- Klik op OK
- Sluit het venster

Nu moeten we ervoor zorgen dat de group `IT` wel aan `Control Panel` kan.
- Ga nu naar de OU `IT` in de rechter kolom
- Rechter klik op de OU `IT` en klik op `Create a GPO in this domain, and Link it here...`
- Geef deze de naam `Allow C&C`
- Rechter klik op de zonet aangemaakte GPO
-  Volg volgende structuur in de linker kolom.
- `User Configuration`-> `Policies`-> `Administrative Templates`-> `Control Panel`
- Dubbel klik nu rechts op `Prohibit access to Control Panel and PC settings`
- Vink Enabled aan
- Klik op Apply
- Klik op OK
-  Volg volgende structuur in de linker kolom.
- `User Configuration`-> `Policies`-> `Administrative Templates`-> `System`
- Dubbel klik nu rechts op `Prevent access to the command prompt`
- Vink Disabled aan
- Klik op Apply
- Klik op OK
- sluit het venster
### Verbied het gebruik van USB-sticks, CDs, DVDs en andere verwijderbare media
- Open `Group Policy Management`
- Ga naar de OU `Employees`
- Maak hier ene nieuwe GPO aan, geef deze de naam `No external drives`
- Rechterklik op de nieuwe GPO en edit
-  Volg volgende structuur in de linker kolom.
- `User Configuration`-> `Policies`-> `Administrative Templates`-> `System` -> `Removable Storage Access`
- Dubbel klik nu rechts op `All Removable Storage classes: Deny all access`
- Vink Disabled aan
- Klik op Apply
- Klik op OK
- Sluit het venster
### Sluit het gastaccount af
- Open `Group Policy Management`
- Ga naar de OU `Employees`
- Maak hier ene nieuwe GPO aan, geef deze de naam `No guests`
- Rechterklik op de nieuwe GPO en edit
-  Volg volgende structuur in de linker kolom.
- `Computer Configuration`-> `Policies`-> `Windows Settings`-> `Security settings` -> `Local Policies` -> `Security Options`
- Dubbel klik nu rechts op `Accounts: Guest account status`
- Vink `Define this policy setting` aan
- Klik op Apply
- Klik op OK
- Sluit het venster
### Verhinder automatische driver-updates.
- Open `Group Policy Management`
- Ga naar de OU `Employees`
- Maak hier ene nieuwe GPO aan, geef deze de naam `No driver updates`
- Rechterklik op de nieuwe GPO en edit
-  Volg volgende structuur in de linker kolom.
- `Computer Configuration`-> `Policies`-> `Administrative Templates`-> `Windows Components` -> `Windows Updates` 
- Dubbel klik nu rechts op `Do not include drivers with Windows Updates`
- Vink `Enabled` aan
- Klik op Apply
- Klik op OK
- Sluit het venster
### Snelkoppeling cosci.be
- Open `Group Policy Management`
- Ga naar de OU `Employees`
- Maak hier ene nieuwe GPO aan, geef deze de naam `No driver updates`
- Rechterklik op de nieuwe GPO en edit
-  Volg volgende structuur in de linker kolom.
- `Computer Configuration`-> `Preferences`-> `Windows settings`-> `Shortcuts` 
- Klik rechts op Shorcuts en kies voor new shortcut
- Name: Cosci.be
- Target Type: URL
- Target URL: cosci.be
- Klik op Apply
- Klik op OK
- Sluit het venster
### Script Logon name
- Maak een bestand aan in `Documents`
- Plak hier volgend script in
```
$gebruiker=$env:USERNAME
whoami >> C:\Users\$gebruiker\log.log
get-date >> C:\Users\$gebruiker\log.log
```
- Sla het bestand op als script.ps1
	- > Indien het opslaan met andere exstensie niet lukt volg volgende stappen.
	 1. Sla het bestand op als een gewoon txt bestand in Documents
	 2. Ga naar File Explorer en klik op Documents
	 3. Klik bovenaan op view
	 4. Vink daar File name exstensions aan
	 5. Nu rename je het bestand script.txt naar script.ps1 
- Open `Group Policy Management`
- Ga naar de OU `Employees`
- Maak hier ene nieuwe GPO aan, geef deze de naam `Logon script`
- Rechterklik op de nieuwe GPO en edit
-  Volg volgende structuur in de linker kolom.
- `User Configuration`-> `Windows settings`-> `Scripts`
- Klik rechts op Logon in de rechterkolom en klik op Properties
- Klik nu op Show Files...
- Er opent nu een File Explorer tablad
- Hierin moet het script komen dat we daarstraks gemaakt hebben
- Kopieer het script en plak het hier
- Sluit dan File Explorer af
> Nu gaan we het bestand koppelen aan het inloggen 
- Klik nu op Add... (in het venster Logon Properties op het tablad Scripts)
- Kies dan voor Browse...
- Dubbelklik het bestand Script.ps1
- Klik op OK
- Klik nu op het tablad PowerShell Scripts
- Kies voor Add..
- Kies voor Browse...
- Dubbelklik op het bestand Script.ps1
- Klik op OK
- Klik nu op Apply en daarna op OK
> Wanneer je nu op je windows 10 client opnieuw inlogd zal er een bestand log.log gemaakt worden in je gebruikers map
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU3NzU2OTc5OCw1MDc5MTE5ODgsNzI3MT
E1NDc3LC0zNjU2MTI0MTgsLTQxNzIxMTI0LC0xMjY1MDQ4MDU0
LDE1NDIyNjgwMTMsLTExMDIwMTQzODksLTE3MjI5Mzc3NzIsMT
Y4NjkwMDY1MCwtMTk3NjYxMjI0Niw5MjMxOTM2MzVdfQ==
-->
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMwMDU1NDEyXX0=
-->