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

Kirjoitin tekstitiedostoon ajettavat tilat 

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/73be53cb-39f7-4b04-8ee0-fc0272cc0d66)

Tämän jälkeen yritin ajaa tiloja 

        $ sudo salt-call --local state.apply

Sain kuitenkin vastaukseksi virheilmoituksen 

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/e8705bd5-5937-4273-ae28-d21a31d446ff)

Päätin luoda uuden kansion ja uuden init.sls-tiedoston

        $ sudo mkdir helloworld
        $ sudoedit init.sls

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/9a804e5e-2fe7-4c38-8078-e6c506a59aa2)

Loin myös toisen uuden kansion



![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/bceece3c-2fd7-4436-b7b8-c3e48e0632a2)

Siirryin takaisin /srv/salt -kansioon muokkaamaan top.sls -tiedostoa

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/633c198f-3ccc-4e51-8464-c2b46285c31f)

Kokeilin ajaa komentoja uudelleen 

        $ sudo salt-call --local state.apply

Onnistui! Hakemistojen nimet ja init.sls -tiedostojen sisältö ei täsmännyt, joten tiloja ei voitu ajaa

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/995fc100-aa27-45f2-8d43-ac8cd5ea190e)

Tähän tehtävään kului aikaa n. 20 minuuttia.

## C) Apache easy mode // Klo 20.35

Lähdin asentamaan Apachea komennolla

        $ sudo apt-get -y install apache2

Asensin tässä välissä curlin

        $ sudo apt-get -y install curl 

Testasin mitä näkyy localhost-sivulla

        $ curl localhost

Sivulla oli näkyvissä Apachen testisivu. Lähdin korvaamaaan testisivua

        $ echo "Kissa" | sudo tee /var/www/html/index.html

Loin uuden kansion ja loin uuden nano-tekstitiedoston, johon täytin Virtual Host-tiedot

        $ sudo mkdir webbi
        $ sudoedit /etc/apache2/sites-available/janiikki.com.conf

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/930cb7bc-5ddf-4ca9-922b-cefd27ecd1ae)

Käynnistin Apachen uudelleen ja siirryin sites-available hakemistoon

        $ sudo systemctl restart apache2
        $ cd /etc/apache2/sites-available/

Suljin default-sivun ja otin luomani sivun käyttöön

        $ sudo a2dissite 000-default.conf
        $ sudo a2ensite janiikki.com.conf 


Käynnistin Apachen uudelleen

        $ sudo systemctl restart apache2

Siirryin webbi-kansioon ja yritin luoda index.html tiedostoa siinä onnistumatta

        $ cd webbi
        $ nano index.html

Koska html-sivuja ei tulisi muokata sudolla, muokkasin hakemiston käyttöoikeuksia

        $ sudo chmow o+w /home/vagrant/webbi/

Lisäsin index.html tiedostoon tekstiä ja käynnistin apachen uudelleen

        $ sudo systemctl restart apache2

Kokeilin curlilla miltä sivulla näyttää

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/15646622-f279-444f-82cc-c3947c9895d9)

Tekstini näkyi sivulla oikein. Lähdin automatisoimaan äskeistä. Loin uuden kansion Salt-hakemistoon ja siirryin sinne

        $ sudo mkdir -p /srv/salt/apache2
        $ cd /srv/salt/apache2

Loin kansioon init.sls-tiedoston, johon kirjoitin Salt-tiloja

        $ nano init.sls

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/b41a2db8-a57c-4c11-9b68-729b80c31a39)


Loin uuden index.html tiedoston /srv/salt/apache2 hakemistoon, kirjoitin sinne Mau

        $ nano index.html

Yritin ajaa Salt-tiloja

        $ sudo salt '*' state.apply apache2

Jostain syystä Salt ei löytänyt index.html-tiedostoa.

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/581c3f18-13ca-46cb-a8d9-12bfa2a6f637)

Tarkistelin Salt-masterin lokitiedostoja, ja löysin sieltä useita virheilmoituksia liittyen verkkoasetuksiin, mutta en tiedä liittyykö tämä suoranaisesti ongelmaani. 

Lopetettu tehtävä klo 20.50.

Jatkoin tehtävää 23.4. klo 14.15


## D) SSHouto

### Lähdeluettelo

Ninotronix. 22.04.2023. How to install apache2 using salt stack. Luettavissa: https://ninotronix.com/devopsnewblogs/index.php/2023/04/22/how-to-install-apache2-using-salt-stack/
