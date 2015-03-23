---
layout: post
title: "Debugging Wifi connection in Linux"
description: ""
category: 
tags: [linux]
---

cat /etc/lsb-release; uname -a
lspci -nnk | grep -iA2 net
lsusb
iwconfig
rfkill list all
lsmod

nm-tool
nmcli nm
RUNNING         STATE           WIFI-HARDWARE   WIFI       WWAN-HARDWARE   WWAN      
running         connected       enabled         enabled    enabled         enabled 

wpa_supplicant -Dnl80211 -iwlan0 -C/var/run/wpa_supplicant/ -c/etc/wpa_supplicant/wpa_supplicant.conf -dd



настроить wifi
# iwpriv wlan0 set_power 7
where wlan0 is the name of your interface. This will reduce idle power consumption by 1-2 Watts compared to no power management. To return to the "normal" operation mode, you can issue:
# iwpriv wlan0 set_power 6.
In order to check current settings, you can issue:
# iwpriv wlan0 get_power.

•To disable the radio (and further reduce power consumption)    when the card is not in use, issue:
# echo 1 > /sys/bus/pci/drivers/ipw2200/*/rf_kill
•To enable the radio, issue:
# echo 0 > /sys/bus/pci/drivers/ipw2200/*/rf_kill


•To make the radio off by default after boot, add
options ipw2200 disablesable=1

# echo options ipw2200 led=1 > /etc/modutils/ipw2200
# update-modules


Run iwconfig eth1 essid off after every wpa_supplicant disconnection.


On linux, forcing a rate reduction was enough to fix the problem (adaptive rate does not seem to work)
iwconfig eth1 rate 1M


https://wireless.wiki.kernel.org/en/users/Drivers/iwlwifi
http://saftware.de/#ipw2200
