# H3 - Toimiva versio

Tämän viikon kotitehtävissä (Karvinen 2024) loin uuden repositorion Githubiin, kloonasin sen koneelleni, tein muutoksia README-tiedostoon ja puskin ne näkymään web-sivulle. Tein "tyhmän" muutoksen README-tiedostoon, jonka jälkeen tuhosin muutokset komennolla ```git reset --hard```. Tutkin gitin lokitiedostoja komennolla ```git log``` ja analysoin niitä. Yritin myös ajaa omia Salt-komentojani virtuaalikoneella. Suoritin tehtävää 11.04. klo 18.10-19.00 sekä 16.04. klo 13.40-16.20. Tähän ei sisältynyt tiivistelmien tekeminen. 

## X) Tiivistelmä

### Chacon and Straub 2014: [Pro Git, 2nd Ed:](https://git-scm.com/book/en/v2) [1.3 Getting Started - What is Git?](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)

- Git näkee datan "snapshotteina" eli tilannekuvina
- Git tarvitsee lähestulkoon ainoastaan paikallisia tiedostoja toimiakseen
- Projektin historian tutkiminen on nopeaa, sillä Git voi lukea sen suoraan tietokannasta
- Git mahdollistaa uusien juttujen kokeilemisen, sillä tietojen kadottaminen on erittäin haastavaa
  

### git add . && git commit; git pull && git push

- Git add - tärkeä komento, joka lisää hakemistoon uusia tiedostoja valmisteltavaksi committia varten (Github 2020)
- Git commit - tämä komento varmistaa, että projektin sen hetkinen tila tallennetaan (Atlassian)
- Git pull - komennolla noudetaan committeja, ja päivitetään etäversiosta tietoa paikalliselle versiolle (FreeCodeCamp 2020)
- Git push - komennon avulla pusketaan muutokset etärepositorioon (Atlassian) 

### Tero Karvisen suolax-repositorion loki ja muutokset

- Repositorioon on tehty kahdeksan committia
- README-fileen on lisäilty tekstiä, sieltä on myös poistettu tekstiä ja lisätty käyttöohjeita
- Make-komennolla voidaan suorittaa Salt-tiloja
(Karvinen 2024)
## A) Online // 12. 04. klo 18.10

Aloitin tehtävän siirtymällä https://github.com/ -verkkosivulle. Lähdin luomaan uutta repositiota, jolle annoin nimen Hello-summer. Kuvaukseen kirjoitin myös tekstin Hello summer. Valitsin public-asetuksen, lisäsin README.filen täpällä, ja valitsin lisenssiksi GNU General Public License v3.0.

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/941d7bed-93ab-4833-9775-9c2b073586cd)

Tähän tehtävään kului aikaa n. 3 minuuttia.

## B) Dolly // 11.04. Klo 18.16

Siirryin juuri luomassani repositoriossa kohtaa Code, josta valitsin kohdan SSH. Kopioin linkin. Avasin Powershellin ylläpitäjän oikeuksin, ja loin hakemiston "summertime". Siirryin hakemistoon.

    $ mkdir summertime
    $ cd summertime

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/a376defd-fa7f-463a-b8b7-f39300e8197c)

Kloonasin repositorion ja siirryin Hello-summer hakemistoon

    $ git clone git@github.com:bhd471/Hello-summer.git
    $ cd hello-summer

Avasin notepadin, jossa tein muutoksia tiedostoon

    $ notepad README.md

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/5d83b352-2550-4f40-ad6b-e4ad9979941f)

Lähdin puskemaan muutoksia palvelimelle 

        $ git add . ; git commit ; git pull ; git push

Tämä avasi Vim-editorin, johon lisäsin lyhyen viestin, joka kertoo mitä muutoksia olen tehnyt


![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/a3aabdc9-b3ef-46f2-8e8a-a45806654607)

Lopputulos: 

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/1692a492-decb-483c-b504-72aef173c7b7)



Tähän tehtävään kului aikaa n. 10 minuuttia

## C) Doh! // Klo 18.36

Avasin README-tiedoston notepadissa tehdäkseni "tyhmän" muutoksen

    $ notepad README.md

Lisäsin tiedostoon satunnaisia kirjaimia ja erikoismerkkejä, tallensin tiedoston

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/6dcd7dfa-c583-4eda-ba08-76e6b394308c)

Tarkistin muutokset 

    $ git status

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/7ac45bb9-a802-4e85-8d8f-8ff008cfdf7e)

Peruutin muutokset 

    $ git reset --hard

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/42a8fe82-9424-4504-afc3-d2c34780dbf9)

Tarkistin myös, että muutokset poistuivat README-tiedostosta.

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/d4c8bd45-6a83-4944-91ba-52f483f21ee1)

Tähän tehtävään kului aikaa n. 8 minuuttia.

## D) Tukki // klo 18.45

Lähdin tarkastelemaan repositorioni loki-tiedostoja

    $ git log

Lokissa näkyy kaksi committia. Toinen on lisäykseni README-tiedostoon. Alempi commit liittyy projektin luomiseen. Sen viesti on "Initial commit", ja tämä on ensimmänen commit jokaisessa projektissa (Stopak 2020). 

Lokitiedostoissa näkyy myös, että Git on osannut arvata oikein nimeni sekä sähköpostiosoitteeni. 
Jos kuitenkin haluaisin muuttaa niitä, se onnistuisi seuraavilla komennoilla:

    $ git config --global user.name "Haluamasi Nimi"
    $ git config --global user.email "haluamasi.sposti@outlook.com"
    
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/27b8d288-9ff8-47e9-9a64-475548dac354)

Tähän tehtävään kului aikaa n. 10 minuuttia

## E) Suolattu rakki // 16.04. Klo 13.40

Tehtävänanto jäi minulle hieman epäselväksi. Yritin kuitenkin parhaani mukaan ratkaista tehtävää.

Aloitin tehtävän kirjautumalla sisään jo olemassaolevalle herra-orja-arkkitehtuurin omaaville virtuaalikoneille

    $ vagrant up
    $ vagrant ssh t001 / master

Loin uuden Salt-hakemiston ja siirryin sinne

    $ mkdir -p /srv/salt
    $ cd /srv/salt/

Loin uuden top.sls tiedoston johon kirjoitin konfiguraation

    $ sudoedit top.sls

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/118bea02-2863-4338-b5c1-24d2401ea717)


Tallensin sen, ja loin uuden hakemiston, siirryin sinne ja loin uuden init.sls tiedoston

    $ mkdir hello
    $ micro init.sls

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/7d10d681-5206-4e04-9c43-1c6cce1575d1)


Hakemistossa näyttää tältä

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/5ae3fbb8-3ae1-4718-b108-6016d84c59a2)


Yritin ajaa Salt-tilaa, siinä onnistumatta

    $ sudo salt-call --local --file-root=/srv/salt state.apply
    
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/6c0b7eb1-8aab-4c68-bc25-b583953410cf)

En saanut tätä mitenkään päin toimimaan, ja aikaa kului tämän tehtäväosion suorittamiseen rehellisesti noin kolme tuntia.

### Oma käyttöympäristö

Oman koneen speksit:

- Acer Nitro N50-620 työasema
- Windows 11 käyttöjärjestelmä
- Intel Core i5-prosessori
- NVIDIA GeForce RTX 3060 Ti-näytönohjain
- 16 Gt RAM-muistia
- 1 TB tallennustilaa

### Lähdeluettelo

Karvinen, T. 2024. H3 - Toimiva versio. Tero Karvisen verkkosivut. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/ Luettu: 11.04.2024.

Stopak, J. 08.04.2020. Initial Commit. What is An Initial Commit In Git? Luettavissa: https://initialcommit.com/blog/What-Is-An-Initial-Commit-In-Git 
Luettu: 11.04.2024.

Github. 2020. Git Guides. Git add. Luettavissa: https://github.com/git-guides/git-add
Luettu 11.04.2024.

Atlassian. Git commit. Luettavissa: https://www.atlassian.com/git/tutorials/saving-changes/git-commit
Luettu: 11.04.2024.

FreeCodeCamp. 27.01.2020. Git Pull Explained. Luettavissa: https://www.freecodecamp.org/news/git-pull-explained/
Luettu: 11.04.2024. 

Atlassian. Git push. Luettavissa: https://www.atlassian.com/git/tutorials/syncing/git-push
Luettu: 11.04.2024.

