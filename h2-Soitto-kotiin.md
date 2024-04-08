# H2 - Soitto kotiin

X) Tiivistelmä

## [Two machine virtual network with Debian 11 Bullseye and Vagrant](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/)

- Vagrantin avulla voidaan luoda uusia virtuaalikoneita minuuteissa
- Voidaan asentaa komennoilla ```sudo apt-get update``` ja ```sudo apt-get install vagrant virtualbox```
- Voimme hallita Vagrantin avulla myös kahta virtuaalikonetta

A) Aloitin tehtävän suorittamisen klo 18.20
Avasin Powershellin ylläpitäjänä, ja siirryin kotihakemistooni komennolla:

        $ cd C:\Users\janik
Loin uuden hakemiston "palvelintenhallinta" ja kansioon hakemiston "twohost"

        mkdir C:\Users\janik\palvelintenhallinta\twohost

Loin Vagrantilla uuden virtuaalikoneen

        $ vagrant init debian/bullseye64



Avasin notepadin, ja loin uuden Vagrantfile-tekstitiedoston

        $ notepad Vagrantfile


        
loin uuden virtuaalikoneen Vagrantin avulla. 

        $ vagrant init debian/bullseye64
        $ vagrant up



![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/81b1d361-a138-4456-955a-d23520248859)

### Lähdeluettelo

Karvinen, T. H2 - Soitto kotiin. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/
Luettu: 08.04.2024.

Karvinen, T. Two Machine Virtual Network With Deabian 11 Bullseye and Vagrant. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/
Luettu: 08.04.2024.

Karvinen, T. 28.03.2018. Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux
Luettu 08.04.2024.

