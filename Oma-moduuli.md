# Oma moduuli

Aloitin luomalla uusia virtuaalikoneita Vagrantin avulla ja nimesin koneita tekemällä muutoksia Vagrantfileen.

    $ vagrant init debian/bullseye64
    $ notepad Vagrantfile

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/55f5ad65-dfb5-4f67-b9f1-7de58489dc25)

klo 15.15-

Sitten koneet käyntiin ja kirjaudutaan sisään. Kokeillaan kirjautua molemmille koneille ssh avulla

        $ vagrant up
        $ vagrant ssh kone1
        $ vagrant exit
        $ vagrant ssh kone2
        
Pingataan koneilla toisiaan, toimii!

        $ vagrant ssh kone1
        $ ping -c 192.168.88.102
        $ exit

        $vagrant ssh kone2
        $ ping -c 1 192.168.88.101
        $ exit

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/06365af0-5754-4c5c-a3ff-08a8467460a1)

Asetetaan "kone1" masteriksi

    $ sudo apt-get update
    $ sudo apt-get -y install salt-master

Tarkistetaan masterin IP-osoite (10.0.2.15 192.168.88.101)

        $ hostname -I

Asetetaan "kone2" orjaksi

    $ sudo apt-get update
    $ sudo apt-get -y install salt-minion

Liitetään koneet yhteen lisäämällä masterin IP-osoite konfiguraatiotiedostoon ja käynnistetään orja uudelleen

        $ sudoedit /etc/salt/minion
        $ sudo systemctl restart salt-minion.service
    
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/77779403-3935-4a0d-914a-079fcb482188)

Hyväksytään orja-avain master koneella

        $ sudo salt-key -A

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/89657170-6045-45f8-826f-7f8621574d4d)

     
### Lähteet

