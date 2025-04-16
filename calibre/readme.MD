# Calibre
## Informatie
Calibre is een tool om epubs te beheren (bibliotheek) en te sideloaden op ereaders. Om Calibre fatsoenlijk te gebruiken in combinatie met Kobo-ereaders, zijn er een paar plugins nodig. Daarnaast heb ik mijn Calibre zo ingericht dat comics in allemaal in een specifieke map terecht komen. Deze map wordt niet geindexeerd door Nickel (de Kobo UI) zodat ze niet zichtbaar zijn. Om de comics te lezen, heb ik KOReader geinstalleerd op mijn Kobo Libra Colour ('KLC') en deze dusdanig ingericht dat KOReader uitsluitend de map met comics laat zien. 

## Comics naar een specifieke map
Op mijn ereader staat in de root de map _Comics. Deze map bevat alle comics (.cbr) die door Calibre op mijn KLC gesideload worden. In het bestand [Kobo eReader.conf](https://github.com/jacobfresco/kobo-misc/blob/main/calibre/Kobo%20eReader.conf) heb ik opgenomen dat deze map niet wordt geindexeerd door Nickel (de Kobo UI) waardoor ze niet zichtbaar zijn als ik in het hoofdscherm van mijn Kobo zit. 

```
[FeatureSettings]
ExcludeSyncFolders=(\\.(?!kobo|adobe).+|_.*|([^.][^/]*/)+\\..+)
```

Iformatie: [https://pgaskin.net/NickelMenu/]

Documentatie: [https://github.com/pgaskin/NickelMenu/blob/v0.5.4/res/doc]

GitHub Repo: [https://github.com/pgaskin/NickelMenu]

Discussie Forum: [https://www.mobileread.com/forums/showthread.php?t=329525]
## Plugins
KoboUtilities
KoboTouch

