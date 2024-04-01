## A) Hello Windows Salt world

Lähtötilanne on se, että Salt on onnistuneesti asennettu työasemalle. Avaan Windows Powershellin pääkäyttäjänä. 

Tarkistin komennolla vielä Saltin asennuksen:

```
$ salt-call --version
```
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/da51970c-dd27-4dfd-a985-e3ac7939a5ad)

## B) Hello Vagrant
Koneelleni on jo asennettu Virtualbox. Lähden asentamaan Vagrantia ja raportoin asennuksen alapuolelle.
### Vagrantin asennus // klo 13.50
Lähden asentamaan Vagrantia. Siirryn sivustolle https://developer.hashicorp.com/vagrant/install . Valitsen Windows-paketin ja lähden suorittamaan asennusta. 

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/b0e738da-ebe8-477e-9048-620069b3f258)
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/27322357-5c62-4157-80dc-7e2442149188)
Latauksessa kesti noin 2 min. Joudun käynnistämään koneeni uudelleen, jotta asennus astuu voimaan. Tähän koko hommaan kului aikaa noin 6 minuuttia.

### Vagrant toimii
Tarkistetaan vielä komennon avulla, että Vagrant toimii:
```
$ vagrant --version
```
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/08562c7f-1632-4f31-af8d-46b1b208e9bc)

## C) Uusi virtuaalikone Vagrantin avulla // klo 14.08
Avaan isäntäkoneellani Powershellin pääkäyttäjän oikeuksin. Luon uuden virtuaalikoneen syöttämällä komentoriville seuraavat komennot:

```
$ vagrant init debian/bullseye64
$ vagrant up
```
Kirjaudun sisään virtuaalikoneelle ssh:n avulla
```
$ vagrant ssh
```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/96b67c16-69aa-4679-a1a6-c70159ddef25)

Tähän kului aikaa noin 5 minuuttia.

## A) Saltin asennus Linuxille // klo 14.16
Lähden asentamaan Saltia juuri luomalleni virtuaalikoneelle.

```
$ sudo apt-get update
$ sudo apt-get install salt-minion
```

Tähän kului aikaa noin 4 minuuttia.

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/1548cdbe-f7d0-4e23-a139-bca84d052238)

## B) Salt ja pkg, file, service, user & cmd // klo 14.22

Aloitin pkg-komennosta. Komennolla voidaan asentaa ja poistaa paketteja (Oracle).


```
$ sudo salt-call --local -l info state.single pkg.installed tree
$ sudo salt-call --local -l info state.single pkg.removed tree
```


![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/f541be23-216f-4c14-b696-f924bd269b99)

_- ID: Komennon tehtävä, tunniste_
_- Function: Mikä funktio on kyseessä_
_- Result: Onnistuiko toimenpide_
_- Comment: Mahdolliset lisätiedot_
_- Started: Milloin toimenpide aloitettiin_
_- Duration: Kauanko toimenpide kesti_
_- Changes: Mahdolliset muutokset_

File-komennolla voidaan hallita tiedostoja (Salt Project, 2024). Tässä tapauksessa luodaan tiedosto.

```
$ sudo salt-call --local -l info state.single file.managed /tmp/moijanika

```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/ea64263b-b248-4f5c-a581-c62fe0fbea21)

- ID: Komennon tehtävä, tunniste
- Function: Mikä funktio on kyseessä
- Result: Onnistuiko toimenpide
- Comment: Mahdolliset lisätiedot
- Started: Milloin toimenpide aloitettiin
- Duration: Kauanko toimenpide kesti
- Changes: Mahdolliset muutokset


Service-komennolla voidaan käynnistää tai sulkea palveluita, tässä tapauksessa tällä komennolla voidaan käynnistää Apache ja muuttaa määrityksiä niin, että se käynnistyy automaattisesti virtuaalikoneen käynnistyessä (Salt Project 2024). Apachea ei kuitenkaan ole asennettuna tälle virtuaalikoneelle. 

```
$ sudo salt-call --local -l info state.single service.running apache2 enable=True
```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/0824d7ee-6c5c-489f-a164-81729a6a4efe)

- ID: Komennon tehtävä, tunniste
- Function: Mikä funktio on kyseessä
- Result: Onnistuiko toimenpide
- Comment: Mahdolliset lisätiedot
- Started: Milloin toimenpide aloitettiin
- Duration: Kauanko toimenpide kesti
- Changes: Mahdolliset muutokset

User-komennolla hallinnoidaan käyttäjätilejä. Alla oleva komento luo uuden käyttäjän.
```
$ sudo salt-call --local -l info state.single user.present janiikki

```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/26655a3c-81ec-40c6-9b79-a4e37826a4a3)

- ID: Komennon tehtävä, tunniste
- Function: Mikä funktio on kyseessä
- Result: Onnistuiko toimenpide
- Comment: Mahdolliset lisätiedot
- Started: Milloin toimenpide aloitettiin
- Duration: Kauanko toimenpide kesti
- Changes: Mahdolliset muutokset
  
Cmd-komennolla hallinnoidaan suoritettuja komentoja. Se voi määrätä komentoja suoritettavaksi tietyissä tilanteissa, tai esimerkiksi tiettyjen ehtojen täytyttyä (Salt Project 2024). Alla oleva komento määrittää, että ´touch /tmp/foo´ luo tiedoston

```
$ sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"

```

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/6291b868-bf1f-4557-b0e1-675a786f1a17)

- ID: Komennon tehtävä, tunniste
- Function: Mikä funktio on kyseessä
- Result: Onnistuiko toimenpide
- Comment: Mahdolliset lisätiedot
- Started: Milloin toimenpide aloitettiin
- Duration: Kauanko toimenpide kesti
- Changes: Mahdolliset muutokset




## Oma käyttöympäristö

Oman koneen speksit:

- Acer Nitro N50-620 työasema
- Windows 11 käyttöjärjestelmä
- Intel Core i5-prosessori
- NVIDIA GeForce RTX 3060 Ti-näytönohjain
- 16 Gt RAM-muistia
- 1 TB tallennustilaa

https://docs.oracle.com/cd/E23824_01/html/E21802/gihhp.html

06.03.2024. https://docs.saltproject.io/en/latest/ref/states/all/salt.states.file.html

06.03.2024. https://docs.saltproject.io/en/latest/ref/states/all/salt.states.cmd.html#execution-of-arbitrary-commands
