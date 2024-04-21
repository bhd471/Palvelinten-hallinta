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

## B) Top

## C) Apache easy mode

## D) SSHouto


