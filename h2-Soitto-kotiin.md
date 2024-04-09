# H2 - Soitto kotiin
Tämän viikon kotitehtävissä (Karvinen 2024) loin kaksi uutta virtuaalikonetta, joita hallitsin samassa verkossa. Asensin näiden koneiden välille master-slave arkkitehtuurin ja suoritin shell-, ja idempotentteja komentoja masterilla master-slave yhteyden yli. Selvitin orjan teknisiä tietoja. Suoritin tehtävän 09.04.2024. klo 11.00-13.45.
X) Tiivistelmä

## [Two machine virtual network with Debian 11 Bullseye and Vagrant](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/)

- Vagrantin avulla voidaan luoda uusia virtuaalikoneita minuuteissa
- Voidaan asentaa komennoilla ```sudo apt-get update``` ja ```sudo apt-get install vagrant virtualbox```
- Luomalla uuden hakemiston ja tallentamalla sinne tiedoston Vagrantfile, voidaan hallita kahta virtuaalikonetta
- Koneille kirjaudutaan ssh-yhteyden avulla ```vagrant ssh koneennimi``
- Uuden koneen luominen ```vagrant up```
- Seuratessa artikkelia ja tehdessä hommia tuntui, että tipuin hieman kärryiltä

## [Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux)

- Saltin avulla voidaan hallita useita virtuaalikoneita
- Voit asentaa masterin komennolla ```sudo apt-get -y install salt-master``` ja slaven komennolla ```sudo apt-get -y install salt-minion```
- Slave Key hyväksytään komennolla ```sudo salt-key -A```
- Mielestäni artikkeli oli helposti seurattava ja riittävän yksinkertainen

## [Hello Salt Infra-as-Code](https://terokarvinen.com/2024/hello-salt-infra-as-code/)

- Luodaan uusi tila, joka varmistaa tekstitiedon olemassaolon
- Uusi moduuli luodaan komennolla ```sudo mkdir -p /srv/salt/hello/```
- Avataan tekstieditori ja lisätään sinne koodia ```sudoedit init.sls```
- Ajetaan ```sudo salt-call --local state.apply hello```


## A) Kaksi virtuaalikonetta samassa verkossa // klo 11.00

Avasin Powershellin ylläpitäjänä, siirryin kotihakemistooni, loin uuden hakemiston "palvelintenhallinta" ja kansioon hakemiston "twohost"


        $ cd C:\Users\janik
        $ mkdir C:\Users\janik\palvelintenhallinta\twohost

        
Loin uuden Vagrant-projektin Linux Debian käyttöjärjestelmällä

        $ vagrant init debian/bullseye64

Avasin tekstieditorin ja liitin sinne konfiguraatiokoodin 

        $ notepad Vagrantfile


![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/e13eb339-1af9-468e-aebb-73c88c33d2d3)

Loin ja käynnistin virtuaalikoneet

        $ vagrant up

![näkymä Virtualboxissa](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/ce7cf57c-f8c0-4ab8-8db8-7c31d93ac878)

Testasin kirjautumista molemmille koneille SSH avulla

        $ vagrant ssh t001
        $ exit
        
        $ vagrant ssh t002
        $ exit

Onnistui!

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

Testasin master-koneella toimiiko

        $ sudo salt '*' cmd.run 'whoami'

Toimii! 

 ![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/7d94df89-3fae-454c-b4ac-466b34277ee6)

 Tähän tehtävään kului aikaa n. 30 minuuttia.

## C) Shell-komento slavella // klo 12.15

Suoritin masterilla komennon, joka listaa hakemistot

        $ sudo salt 'janika' cmd.run 'ls -l'

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/2c56391b-2d26-4f12-b7ca-f5b61e783307)

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/c78ab0da-714a-4a64-9cf3-23c1cacac9b1)


Tähän tehtävään kului aikaa n. 10 minuuttia

## D) Idempotentit komennot // klo 12.25

Suoritan masterilla komennon, joka luo uuden tiedoston. Kun suoritin komennon uudelleen, se ei enää tehnyt mitään, koska asennus oli jo tehty.



        $ sudo salt 'janika' -l info state.single file.managed /tmp/moikka

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/a34054a1-4a8a-4b1d-8604-5bff7922e688)

Tarkistin, että komento onnistui orjassa

        $ vagrant ssh t002
        $ ls -l /tmo/moikka
        
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/cc37bb70-59b8-478a-8646-6cd64cd0cb48)

Suoritan komennon, joka asentaa paketin tree slave-koneelle. Kun suoritin komennon uudelleen, se ei enää tehnyt mitään, koska asennus oli jo tehty.

        $ sudo salt-call 'janika' -l info state.single pkg.installed tree

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/42e67608-0dd1-41b9-b8fa-65f1187d0b33)

Tarkistin asennuksen komennolla 

        $ sudo salt 'janika' cmd.run 'tree --version'
        
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/c52d4216-4f05-4233-9a36-bbe37522340f)

Tähän tehtävään kului aikaa n. 25 minuuttia.

## E) Orjan tekniset tiedot // klo 12.50

Hain master-koneella slaven teknisiä tietoja komennolla 

        $ sudo salt 'janika' grains.items
        
Valitsin tarkempaan tarkasteluun muutamat tiedot

        $ sudo salt 'janika' grains.item os saltversion kernel

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/257fa709-faae-46fe-a51e-6b13c5c1b20e)

> - Kernel: Käyttöjärjestelmän ydin
> - Os: Käyttöjärjestelmä
> - Saltversion: Käytössä oleva versio Saltista

Tähän tehtävään kului aikaa n. 10 minuuttia.

## F) Hello IaC // klo 13.20

Asensin micro-editorin master-koneelle ja asetin sen oletuseditoriksi

        $ sudo apt-get -y install micro
        $ export EDITOR=micro
        
Loin uuden moduulin, jolle annoin nimen 'moimoi' ja siirryin kyseiseen hakemistoon

        $ sudo mkdir -p /srv/salt/moimoi/
        cd /srv/salt/moimoi/

Siirryttyäni hakemistoon suoritin komennon, joka avaa tekstieditorin. Lisäsin tiedostoon idempotenttiä koodia

        $ sudoedit init.sls

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/04ebe5e3-094f-493c-b79c-962430304cd6)


![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/87477c92-cbae-4140-aefd-db0c5e6456b2)

Tämä ei jostain syystä toimi. // Klo 13.30

## Oma käyttöympäristö

Oman koneen speksit:

- Acer Nitro N50-620 työasema
- Windows 11 käyttöjärjestelmä
- Intel Core i5-prosessori
- NVIDIA GeForce RTX 3060 Ti-näytönohjain
- 16 Gt RAM-muistia
- 1 TB tallennustilaa

### Lähdeluettelo

Karvinen, T. H2 - Soitto kotiin. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/
Luettu: 08.04.2024.

Karvinen, T. 04.11.2021. Two Machine Virtual Network With Deabian 11 Bullseye and Vagrant. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/
Luettu: 08.04.2024.

Karvinen, T. 28.03.2018. Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux
Luettu 08.04.2024.

Karvinen, T. 03.04.2024. Hello Salt Infra-as-Code. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2024/hello-salt-infra-as-code/
Luettu 09.04.2024.
