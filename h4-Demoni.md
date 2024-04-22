# H4 - Demoni

## Tiivistelmä

## [Salt Vagrant - Automatically provision one master and two slaves](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file)

- Luodaan init.sls tiedosto ja muokataan sitä
- Huomaa, että sisentämisessä ei käytetä tabia vaan kahta välilyöntiä
- Ajetaan komento ```sudo salt '*' state.apply hello```

- Top- tiedosto määrittää, mitä tiloja orjat ajavat
- Ajetaan komento ```sudo salt '*' state.apply```

## [Salt overview](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml)

- YAML on merkintäkieli, Salt käyttää sitä tietojen käsittelyyn
- Käytetään välilyöntejä, ei tabia
- #- aloittaa kommentin
- YAML koostuu kolmesta osasta, joita ovat skalaarit, listat ja sanakirjat
- YAML jaetaan lohkoihin
- Teksti täytyy sisentää

## [Pkg-File-Service - Control Daemons With Salt - Change SSH Server Port](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh)

- Palvelinten hallintaa Saltilla
- Luodaan uusi SSH tila
- Suorita tila orjalla
- Testaa komennolla ```nc -vz tero.example.com```



## A) Hello SLS!

22.04. klo 20.00

Aloitin kirjautumalla sisään salt masterille

    $ vagrant up
    $ vagrant ssh t001

Loin uuden hakemiston

    $ sudo mkdir -p /srv/salt/hello
    $ cd /srv/salt/hello

Loin init.sls tiedoston, johon kirjoitin komennon

    $ sudoedit init.sls
    
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/0febe42b-d80e-4736-b7af-9199725c0d07)

Hei maailma -tila luotu

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/868c575f-8284-4c34-bad7-f89d0c8b4adf)

Tähän tehtävään kului aika n. 10 minuuttia.

## B) Top // Klo 20.10

Loin uuden kansion hakemistoon ja siirryin sinne

    $ mkdir moivaan
    $ cd moivaan

Loin uuden init.sls-tiedoston, johon kirjoitin uduen tilan

    $ sudoedit init.sls

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/c9091216-5339-4503-bdf2-f0fba0ddb26c)

Siirryin takaisin hakemistoon /srv/salt ja loin sinne top.sls-tiedoston

    $ cd ..
    $ sudoedit top.sls



## C) Apache easy mode

## D) SSHouto


