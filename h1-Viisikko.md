# H1 - Viisikko
Tämän viikon kotitehtävissä (Karvinen 2024) asensin Vagrantin, loin sen avulla uuden virtuaalikoneen ja asensin tälle uudelle koneelle Saltin. Esittelin Saltin tärkeimmät funktiot, tutkin idempotenssia sekä keräsin hieman tietoja uudesta virtuaalikoneestani grains.items-menetelmällä. Suoritin tehtävän 01.04.2024. klo 15.45-18.30.
## X) Tiivistelmä
### [Create a Web Page Using Github](https://terokarvinen.com/2023/create-a-web-page-using-github/)

- Sivun luominen Githubiin on nopeaa ja yksinkertaista
- Kirjaudutaan sisään Githubiin
- Luodaan uusi julkinen repositorio, on tärkeää muistaa luoda myös samalla README-tiedosto
- Siirry repositorioon ja luo uusi tiedosto
- Muista tallentaa sivu "Commit"-napilla

### [Raportin kirjoittaminen](https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/)

- Raporttia tulisi kirjoittaa samalla kun suorittaa
- Sen tulisi olla niin toistettava, että joku voisi tehdä saman asian pelkästään raportin perusteella
- Muista oikeinkirjoitus, väliotsikot sekä lähdeviitteet
  

### [Run Salt Command Locally](https://terokarvinen.com/2021/salt-run-command-locally/)

- Salt voidaan asentaa Linuxille komennoilla ``sudo apt-get update`` ja ``sudo apt-get -y install salt-minion``
- Asennuksen voi tarkistaa komennolla ``sudo salt-call --version``
- Pkg, file, service, user ja cmd ovat tärkeimpiä Salt funktioita
  

## A) Hello Windows Salt world

Lähtötilanne on se, että Salt on onnistuneesti asennettu työasemalle. Avasin Windows Powershellin pääkäyttäjänä. 

Tarkistin vielä komennolla Saltin asennuksen:

```
$ salt-call --version
```
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/da51970c-dd27-4dfd-a985-e3ac7939a5ad)

## B) Hello Vagrant
Koneelleni on jo asennettu Virtualbox. Lähden asentamaan Vagrantia ja raportoin asennuksen alapuolelle.
### Vagrantin asennus // klo 15.50
Lähdin asentamaan Vagrantia. Siirryin sivustolle https://developer.hashicorp.com/vagrant/install . Valitsin Windows-paketin ja lähdin suorittamaan asennusta. 

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/b0e738da-ebe8-477e-9048-620069b3f258)
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/27322357-5c62-4157-80dc-7e2442149188)
Latauksessa kesti noin 2 min. Jouduin käynnistämään koneeni uudelleen, jotta asennus astuu voimaan. Tähän koko hommaan kului aikaa noin 6 minuuttia.

### Vagrant toimii
Tarkistetaan vielä komennon avulla, että Vagrant toimii:
```
$ vagrant --version
```
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/08562c7f-1632-4f31-af8d-46b1b208e9bc)

## C) Uusi virtuaalikone Vagrantin avulla // klo 16.08
Avasin isäntäkoneellani Powershellin pääkäyttäjän oikeuksin. Loin uuden virtuaalikoneen syöttämällä komentoriville seuraavat komennot:

```
$ vagrant init debian/bullseye64
$ vagrant up
```
Kirjauduin sisään virtuaalikoneelle ssh:n avulla
```
$ vagrant ssh
```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/96b67c16-69aa-4679-a1a6-c70159ddef25)

Tähän kului aikaa noin 5 minuuttia.

## A) Saltin asennus Linuxille // klo 16.16
Lähdin asentamaan Saltia juuri luomalleni virtuaalikoneelle.

```
$ sudo apt-get update
$ sudo apt-get install salt-minion
```

Tähän kului aikaa noin 4 minuuttia.

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/1548cdbe-f7d0-4e23-a139-bca84d052238)

## B) Salt ja pkg, file, service, user & cmd // klo 16.22

Aloitin **pkg**-komennosta. Komennolla voidaan asentaa ja poistaa paketteja (Salt Project 2024).


```
$ sudo salt-call --local -l info state.single pkg.installed tree
$ sudo salt-call --local -l info state.single pkg.removed tree
```


![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/f541be23-216f-4c14-b696-f924bd269b99)

> - ID: Komennon tehtävä, tunniste
> - Function: Mikä funktio on kyseessä
> - Result: Onnistuiko toimenpide
> - Comment: Mahdolliset lisätiedot
> - Started: Milloin toimenpide aloitettiin
> - Duration: Kauanko toimenpide kesti
> - Changes: Mahdolliset muutokset

**File**-komennolla voidaan hallita tiedostoja (Salt Project, 2024). Tässä tapauksessa luotiin tiedosto.

```
$ sudo salt-call --local -l info state.single file.managed /tmp/moijanika

```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/ea64263b-b248-4f5c-a581-c62fe0fbea21)

> - ID: Komennon tehtävä, tunniste
> - Function: Mikä funktio on kyseessä
> - Result: Onnistuiko toimenpide
> - Comment: Mahdolliset lisätiedot
> - Started: Milloin toimenpide aloitettiin
> - Duration: Kauanko toimenpide kesti
> - Changes: Mahdolliset muutokset


**Service**-komennolla voidaan käynnistää tai sulkea palveluita, tässä tapauksessa tällä komennolla voidaan käynnistää Apache ja muuttaa määrityksiä niin, että se käynnistyy automaattisesti virtuaalikoneen käynnistyessä (Salt Project 2024). Apachea ei kuitenkaan ole asennettuna tälle virtuaalikoneelle. 

```
$ sudo salt-call --local -l info state.single service.running apache2 enable=True
```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/0824d7ee-6c5c-489f-a164-81729a6a4efe)

> - ID: Komennon tehtävä, tunniste
> - Function: Mikä funktio on kyseessä
> - Result: Onnistuiko toimenpide
> - Comment: Mahdolliset lisätiedot
> - Started: Milloin toimenpide aloitettiin
> - Duration: Kauanko toimenpide kesti
> - Changes: Mahdolliset muutokset

**User**-komennolla hallinnoidaan käyttäjätilejä. Alla oleva komento luo uuden käyttäjän.
```
$ sudo salt-call --local -l info state.single user.present janiikki

```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/26655a3c-81ec-40c6-9b79-a4e37826a4a3)

> - ID: Komennon tehtävä, tunniste
> - Function: Mikä funktio on kyseessä
> - Result: Onnistuiko toimenpide
> - Comment: Mahdolliset lisätiedot
> - Started: Milloin toimenpide aloitettiin
> - Duration: Kauanko toimenpide kesti
> - Changes: Mahdolliset muutokset

**Cmd**-komennolla hallinnoidaan suoritettuja komentoja. Se voi määrätä komentoja suoritettavaksi tietyissä tilanteissa, tai esimerkiksi tiettyjen ehtojen täytyttyä (Salt Project 2024). Alla oleva komento määrittää, että ´touch /tmp/foo´ luo tiedoston

```
$ sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"

```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/6291b868-bf1f-4557-b0e1-675a786f1a17)

> - ID: Komennon tehtävä, tunniste
> - Function: Mikä funktio on kyseessä
> - Result: Onnistuiko toimenpide
> - Comment: Mahdolliset lisätiedot
> - Started: Milloin toimenpide aloitettiin
> - Duration: Kauanko toimenpide kesti
> - Changes: Mahdolliset muutokset

Tähän tehtävään kului aikaa 1,5 tuntia, sisältäen 15 min tauon.

## Idempotenssi // klo 17.50

Idempotenssilla tarkoitetaan IT-maailmassa asiaa, esimerkiksi komentoa, joka voidaan toistaa useita kertoja ja lopputulos pysyy aina samana (Siddharth 2023). Käytän esimerkkinä komentoa, jolla luodaan uusi tiedosto. 

```
$ sudo salt-call --local -l info state.single file.managed /tmp/heijaniikki
```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/969d4cd1-2f71-46b1-ae36-6581b4c8ded3)

Tiedosto luotiin. Jos suoritan komennon uudelleen, mitään muutoksia ei tehdä, sillä tiedosto on jo luotu. Halusin luoda uuden tiedoston, loin sen, ja vaikka suorittaisin saman komennon uudelleen lopputulos pysyy samana.

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/033453b6-4cda-4002-bb21-077fc2feaf19)

Tähän tehtävään kului aikaa noin 15 minuuttia.

## D) Tietoja koneesta // klo 18.05

Keräsin tietojani koneesta grains-items-komennolla:

```
$ salt-call --local grains.items
$ sudo salt-call --local grains.item biosreleasedate biosversion username
```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/a4c6d119-3549-41d7-8a9c-0ead8b37ffde)

> - BIOS release date: ohjelmiston julkaisupäivämäärä
> - BIOS-version: Virtualbox. Virtuaalikone käyttää virtuaalista BIOSia
> - Username: kertoo käyttäjän käyttäjätunnuksen


## Oma käyttöympäristö

Oman koneen speksit:

- Acer Nitro N50-620 työasema
- Windows 11 käyttöjärjestelmä
- Intel Core i5-prosessori
- NVIDIA GeForce RTX 3060 Ti-näytönohjain
- 16 Gt RAM-muistia
- 1 TB tallennustilaa

### Lähdeluettelo

Karvinen, T. 21.03.2024. H1 - Viisikko, Palvelinten hallinta -kurssi. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/
Luettu 01.04.2024.

Karvinen, T. 28.03.2023. Create a Web Page Using Github. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2023/create-a-web-page-using-github/ 
Luettu 01.04.2024.

Karvinen, T. 04.06.2006. Raportin kirjoittaminen. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/
Luettu 01.04.2024.

Karvinen, T. 20.10.2024. Run Salt Command Locally. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/
Luettu 01.04.2024.

Salt Project. 06.03.2024. Installation of packages using os package managers such as yam or apt-get. Salt.states.pkg. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.pkg.html
Luettu 01.04.2024.

Salt Project. 06.03.2024. Operations on regular files, special files, directories and symlinks. Salt.states.file. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.file.html
Luettu 01.04.2024.

Salt Project. 06.03.2024. Execution of arbitrary commands. Salt.states.cmd. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.cmd.html#execution-of-arbitrary-commands
Luettu 01.04.2024.

Siddharth. 18.03.2023. Codementor community. The Power of Idempotency: Understanding it's Significance. Luettavissa: https://www.codementor.io/@sidverma32/the-power-of-idempotency-understanding-its-significance-22zkyc7ci1
Luettu 01.04.2024.
