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

> - cpu_model kertoo koneen prosessorin mallin, tässä tapauksessa Intel Core i3-8145U. 

> - efi-secure-boot false - tarkoittaa, että toiminto ei ole käytössä koneella. Secure boot -toiminto varmistaa, että kone ei käynnistä tuntemattomia ohjelmia, jotka saattavat olla haitallisia (Microsoft 2023).

> - id kertoo koneen nimen. Tässä tapauksessa nimi on LAPTOP-4215EMRG. 

Tähän tehtävään kului aikaa n. 10 minuuttia.

## C) File-toiminto // Klo 15.10

Kokeilin luoda uuden tiedoston file-komennolla

        $ salt-call --local -l info state.single file.managed                         /Windows/temp/moijanika
        

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/74bc7de0-062a-4fcf-99eb-57c9f4a2400e)

Onnistui!

Tähän tehtävään kului aikaa n. 5 minuuttia.

## D) CSI Kerava // Klo 18.40

Tämä tehtävä jäi hieman epäselväksi, mutta yritin tutkia asiaa netistä (ChatGPT & Microsoft). Päädyin suorittamaan alla olevan komennon, joka tulosti polun \Windows\system32\drivers\etc\ sisällön. 

        $ Get-ChildItem -Path C:\Windows\System32\drivers\etc\ -File |             Sort-Object | Select-Object -First 10

> - Get-ChildItem hakee tiedostot
> - -Path C:\Windows\System32\drivers\etc\ kertoo haettavan polun
> - -File rajaa haun tiedostoihin
> - Sort-Object lajittelee tuloksen pienimmästä suurimpaan
> - Select-Object -First 10 näyttää vain 10 ensimmäistä tulosta

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/8c0311a6-8a02-4a4f-b313-5a20747b9698)

Tähän tehtävään kului aikaa n. 20 minuuttia. 

## E) Komennus // Klo 19.00



### Lähteet

Microsoft. 08.02.2023. Secure boot. Luettavissa: https://learn.microsoft.com/en-us/windows-hardware/design/device-experiences/oem-secure-boot. Luettu: 29.04.2024.

Microsoft. Get-ChildItem. Luettavissa: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-childitem?view=powershell-7.4. Luettu: 29.04.2024.
