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

Testasin master-koneella toimiiko

        $ sudo salt '*' cmd.run 'whoami'

Toimii! 

 ![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/7d94df89-3fae-454c-b4ac-466b34277ee6)

 Tähän tehtävään kului aikaa n. 30 minuuttia.

## C) Shell-komento slavella klo 12.15

Suoritin masterilla komennon

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

## F) Hello IaC // Tämä tehtävä puuttuu

### Lähdeluettelo

Karvinen, T. H2 - Soitto kotiin. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/
Luettu: 08.04.2024.

Karvinen, T. Two Machine Virtual Network With Deabian 11 Bullseye and Vagrant. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/
Luettu: 08.04.2024.

Karvinen, T. 28.03.2018. Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux
Luettu 08.04.2024.

