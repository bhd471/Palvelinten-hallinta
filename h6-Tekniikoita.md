# H6 - Benchmark

06.05. klo 19.00
## Tiivistelmä

### [Windows Package Manager](https://docs.saltproject.io/en/latest/topics/windows/windows-package-manager.html)

- Salt tarjoaa Windowsille paketinhallintatyökalun
- Package definition -tiedosto määrittää mm. pakettien versiot ja nimet
- Kloonataan repositorio salt-winrepo-ng
- Luodaan tietokanta
- Ladataan paketteja komennolla ```pkg.install```
- Komennolla ```pkg.list_available``` voidaan tarkastella ladattavissa olevien pakettien versioita
- Paketteja voidaan poistaa komennolla ```pkg.remove```

## A) Paketti Windowsia // Klo 19.15

Lähdin asentamaan Windows package manageria (Salt Project 2024). 

    $ salt-call --local winrepo.update_git_repos
    $ salt-call --local pkg.refresh_db


![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/feec729a-a3b9-46ac-9206-19932e8de75b)

Kokeilin asentaa Dropboxin paketinhallintajärjestelmän avulla

    $ salt-call --local pkg.install "dropbox"

Tämä latautui todella hitaasti. 

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/7b066c15-34e6-4e97-9142-6a7cd034d33d)


## B) Benchmark // Klo 20.10

- Tarkoitus: mitä hyötyä tästä on
- Lisenssi: lisenssi nimi, missä lisenssi lukee mitä tarkoittaa
- tekijä vuosi
- riippucuudet alusta käyttöjärjestelmä pilvi verkkoympäristö
- kiinnostavaa hyödyllinen lopputulos tms
- avoimet kysymykset

### [LAMP-stackia Puppetilla (Pyhäranta 2016)](https://markuspyharanta.com/2016/12/10/palvelinten-hallinta-oma-moduuli/)

- Tarkoitus: Asentaa kaikki ohjelmat kerralla. Säästää aikaa ja jättää vähemmän tehtävää.
- Lisenssi: Käytössä oleva lisenssi on GNU General Public License v3. Lisenssi on ilmoitettu raportin alareunassa lähdeluettelon jälkeen. Kyseessä on avoimen lähdekoodin lisenssi.
- Tekijä ja vuosi: Markus Pyhäranta, 2016
- Riippuvuudet: Xubuntu 16.04, Puppet 3.8.5.
- Kiinnostavaa: LAMP:in lisäksi moduuli asentaa Gedit-editorin
  
### [Firefoxin asennus ja kotisivuksi Netflix (Vepsäläinen 2022)](https://github.com/viivivepsalainen/OMA-PROJEKTI-TILA)

- Tarkoitus: Auttaa ikäihmistä Netflixin käytössä.
- Lisenssi: Käytössä oleva lisenssi on GNU General Public License v3. Lisenssiä ei ole erikseen ilmoitettu tekstissä, mutta GitHub valitun lisenssin tiedoston yläpuolella. Kyseessä avoimen lähdekoodin lisenssi.
- Tekijä ja vuosi: Viivi Vepsäläinen, 2022.
- Riippuvuudet: Linux Ubuntu, Oracle VM.
- Kiinnostavaa: Käyttötarkoitus; helpotusta ikäihmisen arkeen on hyvän mielen juttu.

### [Steamin ja Discordin asentaminen minioneille (Toivanen, 2020)](https://ottotoivanen.wordpress.com/2020/05/21/palvelinten-hallinta-h7/)

- Tarkoitus: Asentaa Steam ja Discord.
- Lisenssi: Ei ole ilmoitettu.
- Tekijä ja vuosi: Otto Toivanen, 2020.
- Riippuvuudet: Virtualbox
- Kiinnostavaa: Lopputulos on mielestäni hyödyllinen


## C) Testbench. 

## D) Viisi ideaa. 

- Spotify ja steam asennus
- Apachen asennus ja oletussivun korvaaminen
- 




### Oma käyttöympäristö

### Lähteet

Pyhäranta, M. 10.12.2016. Palvelinten hallinta - Oma moduuli. Luettavissa: https://markuspyharanta.com/2016/12/10/palvelinten-hallinta-oma-moduuli/. Luettu 06.05.2024.

Vepsäläinen, V. 14.12.2022. OMA-PROJEKTI-TILA. Luettavissa: https://github.com/viivivepsalainen/OMA-PROJEKTI-TILA. Luettu 06.05.2024.

Toivanen, O. 21. 05. 2020. Palvelinten hallinta - h7. Luettavissa: https://ottotoivanen.wordpress.com/2020/05/21/palvelinten-hallinta-h7/. Luettu: 06.05.2024.

Salt Project. 30.04.2024. Windows Package Manager. Luettavissa: https://docs.saltproject.io/en/latest/topics/windows/windows-package-manager.html. Luettu 06.05.2024.
