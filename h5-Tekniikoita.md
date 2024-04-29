# H5 - Tekniikoita

## Tiivistelmä

## A) Saltin asennuksen testaaminen // Klo 14.45

Windows-koneellani oli jo Salt asennettuna, joten testasin asennuksen komennolla

    $ salt-call --local --version

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/2115bdc5-8723-482f-8165-e2140f3813b1)

## B) Grains.items-toiminto Saltilla // Klo 14.55

Suoritin komennon, joka listaa tietoja koneesta

    $ salt-call --local grains.items

Valitsin listasta muutaman kohdan joita halusin analysoida

    $ salt-call --local grains.item efi-secure-boot id cpu_model

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/07f18d2d-bc50-4f3d-b3c5-e790ff9c91fa)

cpu_model kertoo koneen prosessorin mallin, tässä tapauksessa Intel Core i3-8145U. 

efi-secure-boot false - tarkoittaa, että toiminto ei ole käytössä koneella. Secure boot -toiminto varmistaa, että kone ei käynnistä tuntemattomia ohjelmia, jotka saattavat olla haitallisia (Microsoft 2023).

id kertoo koneen nimen. Tässä tapauksessa nimi on LAPTOP-4215EMRG. 

Tähän tehtävään kului aikaa n. 10 minuuttia.

## C) File-toiminto // Klo 15.10



### Lähteet

Microsoft. 08.02.2023. Secure boot. Luettavissa: https://learn.microsoft.com/en-us/windows-hardware/design/device-experiences/oem-secure-boot. Luettu: 29.04.2024.
