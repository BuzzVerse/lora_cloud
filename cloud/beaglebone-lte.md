# 🌐 Beaglebone LTE

LTE sticki od Huawei w wersji "s" non-hilink wspierają połączenie przez NDIS (Network Driver Interface Specification):

{% code title="/etc/network/interfaces" %}
```bash
allow-hotplug wwan0
iface wwan0 inet dhcp
      pre-up sleep 1
      pre-up echo -e "AT^SYSCFGEX=\"03\",3FFFFFFF,1,2,800C5,,\r" > /dev/ttyUSB0
      pre-up echo -e "AT^NDISDUP=1,1,\"internet\"\r" > /dev/ttyUSB0
      pre-down echo -e "AT^NDISDUP=1,0\r" > /dev/ttyUSB0
```
{% endcode %}

{% hint style="info" %}
Konfiguracja APN jest dla sieci Play
{% endhint %}
