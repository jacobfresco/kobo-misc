# Calibre
## Informatie
Calibre is een tool om epubs te beheren (bibliotheek) en te sideloaden op ereaders. Om Calibre fatsoenlijk te gebruiken in combinatie met Kobo-ereaders, zijn er een paar plugins nodig. Daarnaast heb ik mijn Calibre zo ingericht dat comics in allemaal in een specifieke map terecht komen. Deze map wordt niet geindexeerd door Nickel (de Kobo UI) zodat ze niet zichtbaar zijn. Om de comics te lezen, heb ik KOReader geinstalleerd op mijn Kobo Libra Colour ('KLC') en deze dusdanig ingericht dat KOReader uitsluitend de map met comics laat zien. 

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

## Plugins

- KoboUtilities: [GitHub](https://github.com/majutsushi/kobo-utilities/tree/main) | [Plugin Forum](https://www.mobileread.com/forums/showthread.php?t=215339)
- SmartEject: [GitHub](https://github.com/JimmXinu/SmartEject) | [Plugin Forum Thread](https://www.mobileread.com/forums/showthread.php?t=192950&page=8)
- Count Pages: [GitHub](https://github.com/kiwidude68/calibre_plugins/tree/main/count_pages) | [Plugin Forum Thread](https://www.mobileread.com/forums/showthread.php?t=134000)


### Kobo Utilities
Met deze plugin maak je de toch al krachtige combinatie Calibre - Kobo ereader nog krachtiger. Je kan je epubs automatisch laten converteren naar kepub voordat deze naar de Kobo worden gesynchroniseerd. Dit zorgt op de Kobo voor lees statistieken per boek en een snellere leeservating. Wil je een meer in-depth vergelijking tussen de twee formaten, lees dan [deze forum thread](https://www.mobileread.com/forums/showthread.php?t=343765) op MobileRead. 

Kobo Utilities allows you to setting the collection for a book, as opposed to doing it manually on the Kobo itself. Also, it syncs the reading progress back to Calibre for you to see. You can backup the .sqlite database if you want. In case of a factory reset, you can just copy it back and have all your reading stats back. 

### Smart Eject
Deze plugin geeft je de mogelijkheid om bij het loskoppelen van de Kobo (iets wat je echt moet doen om crashes en data verlies te voorkomen) de boeken te tonen die of niet op de Kobo staan, maar wel in Calibre, of andersom; de boeken die wel in Calibre staan en niet op de Kobo. Dit maakt het mogelijk om snel te controleren welke boeken er eventueel nog gesynchroniseerd moeten worden (of niet, dat kan natuurlijk ook)

### Count Pages
Deze plugin download het aantal pagina's en woorden in een (k)epub en slaat deze data op in de meta van het bestand. Deze metadata wordt vervolgens gesynchroniseerd naar de Kobo.

## Software

Calibre
KOReader
Kobo Annotation Exporter

