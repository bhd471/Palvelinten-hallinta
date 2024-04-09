# H2 - Soitto kotiin

X) Tiivistelmä

## [Two machine virtual network with Debian 11 Bullseye and Vagrant](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/)

- Vagrantin avulla voidaan luoda uusia virtuaalikoneita minuuteissa
- Voidaan asentaa komennoilla ```sudo apt-get update``` ja ```sudo apt-get install vagrant virtualbox```
- Voimme hallita Vagrantin avulla myös kahta virtuaalikonetta

## A) Aloitin tehtävän suorittamisen klo 11.00

Avasin Powershellin ylläpitäjänä, ja siirryin kotihakemistooni komennolla:

        $ cd C:\Users\janik
Loin uuden hakemiston "palvelintenhallinta" ja kansioon hakemiston "twohost"

        mkdir C:\Users\janik\palvelintenhallinta\twohost



        
Loin uuden Vagrant-projektin Linux Debian käyttöjärjestelmällä

        $ vagrant init debian/bullseye64

Avasin tekstieditorin ja liitin sinne konfiguraatiokoodin 

        $ notepad Vagrantfile


![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/e13eb339-1af9-468e-aebb-73c88c33d2d3)

Luon ja käynnistän virtuaalikoneet

        $ vagrant up

![näkymä Virtualboxissa](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/ce7cf57c-f8c0-4ab8-8db8-7c31d93ac878)

Testaan kirjautumista molemmille koneille SSH avulla

        $ vagrant ssh t001
        $ exit
        
        $ vagrant ssh t002
        $ exit
Onnistuu!

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/0457005f-5ae7-4506-88d3-ad5233f77665)

Kirjauduin sisään koneisiin ja kokeilin pingata toista konetta

        $ vagrant ssh t001
        $ ping -c 192.168.88.102
        $ exit

        $vagrant ssh t002
        $ ping -c 1 192.168.88.101
        $ exit
        
Tämä onnistui.

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/4a2c94d1-2b35-432a-a879-93a37c31051e)

Tähän tehtävään kului aikaa n. 25 minuuttia.

## B) Salt master-slave // klo 11.30

Siirryin koneelle t001 ja tein siitä masterin. Päivitin pakettilistat, asensin salt-masterin ja tarkistin ip-osoitteen (10.0.2.15 192.168.88.101)

        $ vagrant ssh t001
        $ sudo apt-get update
        $ sudo apt-get -y install salt-master
        $ hostname -I 

Tämän jälkeen siirryin koneelle t002 ja tein siitä slaven. Päivitin pakettilistat ja asensin salt-minionin

        $ vagrant ssh t002
        $ sudo apt-get update
        $ sudo apt-get -y install salt-minion
        
Yhdistin masterin ja slaven kirjoittamalla tekstitiedostoon masterin IP-osoitteen. Käynnistin slaven uudelleen, jotta se yhdistyy masteriin

        $ sudoedit /etc/salt/minion
        
        $ sudo systemctl restart salt-minion.service
        
Kirjauduin sisään master-koneelle hyväksyäkseni slave keyn

        $ vagrant ssh t001
        $ sudo salt-key -A

 
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/82247971-630e-46ae-8368-4b8bec5d32d1)

### Lähdeluettelo

Karvinen, T. H2 - Soitto kotiin. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/
Luettu: 08.04.2024.

Karvinen, T. Two Machine Virtual Network With Deabian 11 Bullseye and Vagrant. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/
Luettu: 08.04.2024.

Karvinen, T. 28.03.2018. Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux
Luettu 08.04.2024.

