# kobo-patch
## Over Kobo Patch
Kobo-Patch is een verzameling patches voor Kobo ereaders die het mogelijk maken om bepaalde instellingen en onderdelen in de layout aan te passen naar je eigen smaak.

Informatie: [https://pgaskin.net/kobopatch-patches/]

GitHub Repo: [https://github.com/pgaskin/kobopatch-patches]

Discussie Forum: [https://www.mobileread.com/forums/showpost.php?p=3774914]

## Mijn actieve patches
### 📁 [nickel.yaml](https://github.com/jacobfresco/kobo-misc/blob/main/kobo-patch/nickel.yaml)
Dictionary pop-up - increase available text area:
  - Enabled: yes
  - Description: |
      Increase the area available for dictionary definitions in the dictionary pop-up
      by reducing some of the excess whitespace used (header, footer, margins).
      This patch was formerly known as 'Dictionary pop-up frame size increase', but in
      fw 4.10.11591, Kobo removed access to the code which specifies pop-up frame size.
      fw 4.12.12111, Kobo removed access to the code which could reduce footer size.
      fw 4.20.14601  Kobo added new DictionaryViewFooter CSS stream to control footer height again.

Remove footer (row3) and increase cover size on new home screen:
  - Enabled: yes
  - PatchGroup: Home screen layout tweaks
  - Description: |
      Combines two patches together which share the same PatchGroup:
      - `Increase home screen cover size`
      - `Remove footer (row3) on new home screen`

