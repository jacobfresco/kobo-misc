# nickel-menu
## Informatie
NickelMenu is een volledig aanpasbaar menu voor Kobo ereaders (Nickel). Het draait naast het 'gewone' menu van de ereader

Informatie: [https://pgaskin.net/NickelMenu/]

Documentatie: [https://github.com/pgaskin/NickelMenu/blob/v0.5.4/res/doc]

GitHub Repo: [https://github.com/pgaskin/NickelMenu]

Discussie Forum: [https://www.mobileread.com/forums/showthread.php?t=329525]
## Mijn NickelMenu config
### 📁 [nm_menu.conf](https://github.com/jacobfresco/kobo-misc/blob/main/nickel-menu/nm_menu.conf)
```
##########################################
######## NickelMenu configuration ########
##########################################

#
## Main Menu
menu_item: main : Comics (KOReader) : cmd_spawn : quiet : exec /mnt/onboard/.adds/koreader/koreader.sh
menu_item: main : Mijn artikelen (Pocket) : nickel_open: library : pocket 
menu_item : main : USB Connect : nickel_misc : force_usb_connection
menu_item : main : Rescan Books Full (reboot) : nickel_misc : rescan_books_full
    chain_success : power : reboot
    chain_failure: dbg_error : Rescan failed. 
menu_item : main : Force WiFi on : nickel_setting : toggle: force_wifi
  chain_success : nickel_wifi : toggle
menu_item : main : Free Memory : cmd_output : 500 : free -m
menu_item : main : IP Address : cmd_output : 500 : /sbin/ifconfig | /usr/bin/awk '/inet addr/{print substr($2,6)}'
menu_item : main : Kernel Version : cmd_output : 500 : uname -a
menu_item : main : Screensaver Status : cmd_output : 500 : quiet : test -e /mnt/onboard/.kobo/screensaver_old
  chain_success : dbg_toast : Screensaver is off
  chain_failure : dbg_toast : Screensaver is on
menu_item : main : Toggle screensaver : cmd_output : 500 : quiet : test -e /mnt/onboard/.kobo/screensaver_old
  chain_failure : skip : 3
  chain_success : cmd_spawn : quiet: mv /mnt/onboard/.kobo/screensaver_old /mnt/onboard/.kobo/screensaver
  chain_success : dbg_toast : Screensaver on
  chain_always : skip : -1
  chain_failure : cmd_spawn : quiet: mv /mnt/onboard/.kobo/screensaver /mnt/onboard/.kobo/screensaver_old
  chain_success : dbg_toast : Screensaver off
menu_item : main : Dump Syslog : cmd_spawn : logread > /mnt/onboard/.adds/syslog.log
menu_item : main : Screenshots : nickel_setting : toggle : screenshots
menu_item : main : Whose Kobo is this? : dbg_msg : Jacob Fresco +316 513 98 742
menu_item : main : Reading stats : nickel_open : reading_life:stats
menu_item : main : Reboot : power : reboot
menu_item : main : Shutdown : power : shutdown

#
## Reader Menu
#
menu_item : reader : Free Memory : cmd_output : 500 : free -m
menu_item : reader : Dark Mode : nickel_setting : toggle : dark_mode
menu_item : reader : Invert & Reboot : nickel_setting : toggle : invert
    chain_success : power : reboot
menu_item : reader : Screenshots : nickel_setting : toggle : screenshots
menu_item : reader : Home : nickel_misc : home


#
## Browser Menu
#
menu_item : browser : Maps (popup) : nickel_browser : modal:https://www.google.com/maps/
menu_item : browser : Maps (full) : nickel_browser : https://www.google.com/maps/
menu_item : browser : Wikipedia (popup) : nickel_browser: modal: https://www.wikipedia.org/
menu_item : browser : Wikipedia (full) : nickel_browser : https://www.wikipedia.org/
menu_item : browser : Quit : nickel_misc : home
menu_item : browser : Invert & Reboot : nickel_setting : toggle: invert
    chain_success : power : reboot


#
## Library Menu
#
menu_item : library : USB Connect : nickel_misc : force_usb_connection
menu_item : library : Free Memory : cmd_output : 500 : free -m
menu_item : library : Dark Mode : nickel_setting : toggle : dark_mode
menu_item : library : Invert & Reboot : nickel_setting : toggle : invert
    chain_success : power : reboot
menu_item : library : Screenshots : nickel_setting : toggle : screenshots
menu_item : library : Reboot : power : reboot
menu_item : library : Shutdown : power : shutdown
menu_item : library : Shutdown : power : shutdown

#
## Selection Menu
#
menu_item : selection : Google Translate : nickel_browser : modal : https://translate.google.com/m?sl=auto&tl=nl&q={1||%}
menu_item : selection : Wikipedia Zoeken: nickel_browser : modal : https://m.wikipedia.org/w/index.php?search={1||%}&title=Speciaal%3AZoeken&ns0=1
#
## Selection Search Menu
#
menu_item : selection_search : Google Translate : nickel_browser : modal : https://translate.google.com/m?sl=auto&tl=nl&q={1||%}
menu_item : selection_search : Wikipedia Zoeken : nickel_browser : modal : https://m.wikipedia.org/w/index.php?search={1||%}&title=Speciaal%3AZoeken&ns0=1
#
## Experimental menu settingsd
#
experimental :menu_main_15505_label :Jaap
experimental :menu_main_15505_icon :/mnt/onboard/.adds/nm/.icon.png
```
