# Calibre in combinatie met een Kobo ereader
## Calibre
### Informatie
Calibre is een tool om epubs te beheren (bibliotheek) en te sideloaden op ereaders. Om Calibre fatsoenlijk te gebruiken in combinatie met Kobo-ereaders, zijn er een paar plugins nodig. Het is uiteraard niet verplicht, maar het maakt het leven zo veel simpeler, dat ik het iedereen zou aanraden. 

Download: [Calibre 8.2.100](https://calibre-ebook.com/download)

## Sideload mode
Standaard moet je bij het eerste gebruik van een Kobo een account opgeven voor het syncen. Als je dat, net als ik, eigenlijk niet ziet zitten, dan is er een work-around voor. In het bestand 📁[Kobo eReader.conf](https://github.com/jacobfresco/kobo-misc/blob/main/calibre/Kobo%20eReader.conf) staat de optie `SideloadedMode`. Als je die op 'true' zet, dan vervalt deze hele eis en kan je alleen nog maar boeken op je ereader zetten via USB. 

```
SideloadedMode=true
```
Bijkomend voordeel is dat met deze optie de 'homepage' van Kobo, waar ook de reclame voor luisterboeken en Kobo Plus staat, verdwijnt. Mocht je deze pagina wel willen blijven zien, maar wel van de twee genoemde reclames af willen, dan kan dat via [KoboPatch](https://github.com/jacobfresco/kobo-misc/tree/main/kobo-patch)

## Plugins

- KoboUtilities: [GitHub](https://github.com/majutsushi/kobo-utilities/tree/main) | [Plugin Forum](https://www.mobileread.com/forums/showthread.php?t=215339)
- SmartEject: [GitHub](https://github.com/JimmXinu/SmartEject) | [Plugin Forum Thread](https://www.mobileread.com/forums/showthread.php?t=192950&page=8)
- Count Pages: [GitHub](https://github.com/kiwidude68/calibre_plugins/tree/main/count_pages) | [Plugin Forum Thread](https://www.mobileread.com/forums/showthread.php?t=134000)


### Kobo Utilities
Met deze plugin maak je de toch al krachtige combinatie Calibre - Kobo ereader nog krachtiger. Je kan je epubs automatisch laten converteren naar kepub voordat deze naar de Kobo worden gesynchroniseerd. Dit zorgt op de Kobo voor lees statistieken per boek en een snellere leeservaring. Wil je een meer in-depth vergelijking tussen de twee formaten, lees dan [deze forum thread](https://www.mobileread.com/forums/showthread.php?t=343765) op MobileRead. 

Kobo Utilities geeft je de mogelijkheid om boeken in Calibre toe te voegen aan een verzameling ('collecties'). Normaal gesproken doe je dit per boek op de Kobo zelf. Ook synct de plugin de leesvoortgang terug naar Calibre (percentage gelezen, nog te lezen tijd, gelezen tijd etc.). De .sqlite database op de Kobo kan met deze plugin worden gebackupped waardoor je deze ook weer kan terugzetten na een (onvrijwillige) factory reset.

### Smart Eject
Deze plugin geeft je de mogelijkheid om bij het loskoppelen van de Kobo (iets wat je echt moet doen om crashes en data verlies te voorkomen) de boeken te tonen die of niet op de Kobo staan, maar wel in Calibre, of andersom; de boeken die wel in Calibre staan en niet op de Kobo. Dit maakt het mogelijk om snel te controleren welke boeken er eventueel nog gesynchroniseerd moeten worden (of niet, dat kan natuurlijk ook)

### Count Pages
Deze plugin download het aantal pagina's en woorden in een (k)epub en slaat deze data op in de meta van het bestand. Deze metadata wordt vervolgens gesynchroniseerd naar de Kobo.

## Comics naar een specifieke map
Op mijn ereader staat in de root de map _Comics. Deze map bevat alle comics (.cbr) die door Calibre op mijn KLC gesideload worden. In het bestand 📁 [Kobo eReader.conf](https://github.com/jacobfresco/kobo-misc/blob/main/calibre/Kobo%20eReader.conf) heb ik opgenomen dat deze map niet wordt geindexeerd door Nickel (de Kobo UI) waardoor ze niet zichtbaar zijn als ik in het hoofdscherm van mijn Kobo zit. 

```
[FeatureSettings]
ExcludeSyncFolders=(\\.(?!kobo|adobe).+|_.*|([^.][^/]*/)+\\..+)
```

Om ervoor te zorgen dat Calibre alleen comics in deze map zet en epubs op de standaard manier sideloaded naar de KLC, heb ik een aangepaste template gemaakt die kijkt naar de custom column '#iscomic' in Calibre. Staat deze op Ja/Yes, dan wordt de comic in /_Comics geplaatst.

```calibre
program:
	if check_yes_no("#iscomic", 0 , 0 , 1) then
		'_Comics/' & field('title') & ' - ' & field('authors')
	else
		field('author_sort') & '/' & field('title') & ' - ' & field('authors')
	fi
```

### KOReader
Om de comics te lezen gebruik ik KOReader, een alternatieve lezer voor de Kobo firmware. De laatste versie kan je vinden op de [GitHub-repo](https://github.com/koreader/koreader/releases). KOReader ziet er wat minder gelikt uit dan de Nickel UI van Kobo zelf, maar heeft wel veel meer mogelijkheden om de leeservaring helemaal in te stellen naar eigen wens. Voor mij werkt (voor boeken) de Nickel UI prima, maar anderen zweren bij KOReader. Om KOReader te starten heb ik een entry gemaakt in 📁 [Nickel Menu](https://github.com/jacobfresco/kobo-misc/tree/main/nickel-menu)

```
## Main Menu
menu_item: main : Comics (KOReader) : cmd_spawn : quiet : exec /mnt/onboard/.adds/koreader/koreader.sh
```
Ook KOReader slaat z'n instellingen 'gewoon' op een text-based bestand. Dit bestand is 📁 [settings.reader.lua](https://github.com/jacobfresco/kobo-misc/blob/main/calibre/settings.reader.lua) en is te vinden in /.adds/koreader. Als je mijn versie bekijkt, zul je zien dat ik in KOReader de directory heb 'gelocked' op /_Comics. Op die manier kan ik niet per ongeluk uit de directory komen en ineens boeken aanklikken (OCD, ik weet het). 

## Overige software

### Kobo Annotation Exporter
Mijn Kobo Libra Colour heeft de mogelijkheid om annotaties te maken (indien je een ondersteunde stylus gebruikt). Helaas heeft Kobo (nog) niet goed nagedacht over het exporteren van deze annotaties. Dus ben ik er zelf maar ingedoken. Ik heb redelijk wat ervaring met programmeren, maar in dit geval heb ik het overgelaten aan 🌐[cursor AI](https://cursor.com). Het resultaat: de Kobo Annotation Exporter.

Het is voor nu nog een redelijk simpele oplossing. Kleuren worden nog niet ondersteund en de export is in alle gevallen naar Joplin (omdat ik die app religieus gebruik voor zo'n beetje alles). In de toekomst is het de bedoeling dat je ook 'gewoon' naar een map of HTML kan exporteren. Mocht je nu Joplin gebruiken en zitten te springen om je annotaties te exporeren, je kan Kobo Annotation Exporter downloaden in de [GitHub-repo](https://github.com/jacobfresco/kobo-annotation-exporter)

Release download: [GitHub](https://github.com/jacobfresco/kobo-annotation-exporter/releases/tag/kobo) / [Changelog](https://github.com/jacobfresco/kobo-annotation-exporter/commits/kobo)
