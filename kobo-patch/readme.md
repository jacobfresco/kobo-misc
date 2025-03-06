# kobo-patch
### nickel.yaml
Dictionary pop-up - increase available text area:
  - Enabled: yes
  - Description: |
      Increase the area available for dictionary definitions in the dictionary pop-up
      by reducing some of the excess whitespace used (header, footer, margins).
      This patch was formerly known as 'Dictionary pop-up frame size increase', but in
      fw 4.10.11591, Kobo removed access to the code which specifies pop-up frame size.
      fw 4.12.12111, Kobo removed access to the code which could reduce footer size.
      fw 4.20.14601  Kobo added new DictionaryViewFooter CSS stream to control footer height again.
