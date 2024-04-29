# H5 - Tekniikoita

## Tiivistelmä

Tämän viikon kotitehtävissä (Karvinen 2024) testasin Saltin asennuksen Windowsilla, keräsin tietoa Windows-koneesta grains.items -komennolla, kokeilin Windowsilla file-toimintoa ja tarkastelin viimeksi muokattuja tiedostoja Linuxin find-komennolla. Viimeistä tehtävää, jossa tehtävänantona oli luoda Salt-tila, jolla voidaan asentaa järjestelmään uusi komento, en osannut suorittaa. Suoritin kohdat a, b ja c poikkeuksellisesti läppärillä. Suoritin tehtävän 29.04.2024. klo 14.45-15.15 & klo 19.30-19.50.

### [H5 - Salt Linux tehtävät, Toni Seppä](https://salthomework.wordpress.com/h5/)

- Tehdään Windows 10 Salt-slave
- Ladataan Salt-minion koneelle ja annetaan asennuksessa pilvipalvelimen IP-osoite
- Tarkistetaan ja hyväksytään orja komennoilla ```sudo salt-key ``` &   ```sudo salt-key A```
- Pingataan Saltia Windowsilla  ```./salt-call --local test.ping ```
- Muutetaan päivämääriä komennolla  ```sudo salt ‘tontsa00 salt-minion’ system.set_system_date ‘1977-06-22’```
  


## A) Saltin asennuksen testaaminen // Klo 14.45

Windows-koneellani oli jo Salt asennettuna, joten testasin asennuksen komennolla. 


    $ salt-call --local --version

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/2115bdc5-8723-482f-8165-e2140f3813b1)

## B) Grains.items-toiminto Saltilla // Klo 14.55

Suoritin komennon, joka listaa tietoja koneesta.

    $ salt-call --local grains.items

Valitsin listasta muutaman kohdan joita halusin analysoida

    $ salt-call --local grains.item efi-secure-boot id cpu_model

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/07f18d2d-bc50-4f3d-b3c5-e790ff9c91fa)

> - cpu_model kertoo koneen prosessorin mallin, tässä tapauksessa Intel Core i3-8145U. 

> - efi-secure-boot false - tarkoittaa, että toiminto ei ole käytössä koneella. Secure boot -toiminto varmistaa, että kone ei käynnistä tuntemattomia ohjelmia, jotka saattavat olla haitallisia (Microsoft 2023).

> - id kertoo koneen nimen. Tässä tapauksessa nimi on LAPTOP-4215EMRG. 

Tähän tehtävään kului aikaa n. 10 minuuttia.

## C) File-toiminto // Klo 15.10

Kokeilin luoda uuden tiedoston file-komennolla. 


        $ salt-call --local -l info state.single file.managed                         /Windows/temp/moijanika
        

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/74bc7de0-062a-4fcf-99eb-57c9f4a2400e)

Onnistui!

Tähän tehtävään kului aikaa n. 5 minuuttia.

## D) CSI Kerava // Klo 19.30

Hain viimeksi muokatut tiedostot ensin /etc -hakemistosta ja sitten kotihakemistostani. Rajasin komennon näyttämään vain viisi viimeisintä muutosta

        $ sudo find /etc -printf '%T+ %p\n'|sort | tail -n 5
        $ sudo find $HOME -printf '%T+ %p\n'|sort | tail -n 5
        

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/c85fd076-14a8-44d9-900f-0ce5f0e2ac2c)

> - find = Etsii tiedostoja
> - /etc ja $HOME = hakemistopolut
> - printf = tulostusmuodon määritys
> - sort = lajittelee tuloksen aakkosjärjestykseen
> - tail -n 5 = näyttää vain viisi viimeisintä tiedostoa

Tähän tehtävään kului aikaa n. 20 minuuttia.

## E) Komennus // Klo 19.50

Tätä tehtävää en osannut suorittaa. 

### Oman koneen speksit:

- Acer Nitro N50-620 työasema
- Windows 11 käyttöjärjestelmä
- Intel Core i5-prosessori
- NVIDIA GeForce RTX 3060 Ti-näytönohjain
- 16 Gt RAM-muistia
- 1 TB tallennustilaa


### Lähteet

Karvinen, T. 21.03.2024. H5 - Tekniikoita. Palvelinten hallinta -kurssi. Tero Karvisen kotisivut. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/. Luettu: 29.04.2024.

Microsoft. 08.02.2023. Secure boot. Luettavissa: https://learn.microsoft.com/en-us/windows-hardware/design/device-experiences/oem-secure-boot. Luettu: 29.04.2024.

Microsoft. Get-ChildItem. Luettavissa: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-childitem?view=powershell-7.4. Luettu: 29.04.2024.

Seppä, T. 28.04.2019. H5. Salt linux tehtävät Toni Seppä. Luettavissa: https://salthomework.wordpress.com/h5/. Luettu: 29.04.2024.
