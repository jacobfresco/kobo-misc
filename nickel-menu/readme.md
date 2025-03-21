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
menu_item : library : USB Connect : nickel_misc : force_usb_connection
menu_item : main : Dark Mode : nickel_setting : toggle : dark_mode
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
menu_item :main    :FTP                :cmd_spawn          :quiet:/usr/bin/pkill -f "^/usr/bin/tcpsvd -E 0.0.0.0 1021" || true && exec /usr/bin/tcpsvd -E 0.0.0.0 1021 /usr/sbin/ftpd -w -t 30 /mnt/onboard
  chain_success                        :dbg_toast          :Started FTP server for KOBOeReader partition on port 1021.
menu_item : main : Dump Syslog : cmd_spawn : logread > /mnt/onboard/.adds/syslog.log
menu_item : main : Screenshots : nickel_setting : toggle : screenshots
menu_item : main : Reboot : power : reboot


#
## Reader Menu
#
menu_item : reader : Free Memory : cmd_output : 500 : free -m
menu_item : reader : Mijn artikelen : nickel_open: library: pocket
menu_item : reader : Dark Mode : nickel_setting : toggle : dark_mode
menu_item : reader : Invert & Reboot : nickel_setting : toggle : invert
    chain_success : power : reboot
menu_item : reader : Screenshots : nickel_setting : toggle : screenshots


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
menu_item : library : Free Memory : cmd_output : 500 : free -m
menu_item : library : USB Connect : nickel_misc : force_usb_connection
menu_item : library : Mijn artikelen : nickel_open : library : pocket
menu_item : library : Dark Mode : nickel_setting : toggle : dark_mode
menu_item : library : Invert & Reboot : nickel_setting : toggle : invert
    chain_success : power : reboot
menu_item : library : Screenshots : nickel_setting : toggle : screenshots
menu_item : library : Reboot : power : reboot
menu_item : library : Shutdown : power : shutdown

#
## Selection Menu
#
menu_item : selection : Google Translate : nickel_browser : modal : https://translate.google.com/m?sl=auto&tl=en&q={1||%}

#
## Selection Search Menu
#
menu_item : selection_search : Google Translate : nickel_browser : modal : https://translate.google.com/m?sl=auto&tl=en&q={1||%}

#
## Experimental menu settingsd
#
experimental :menu_main_15505_label :Jaap
experimental :menu_main_15505_icon :/mnt/onboard/.adds/nm/.icon.png
```
