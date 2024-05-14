# Oma moduuli

Tämän moduulin tarkoituksena on helpottaa ja nopeuttaa asennuksia.

Lisenssi: 

Aloitin luomalla kaksi uutta virtuaalikonetta Vagrantin avulla. Määritin koneet tekemällä muutoksia Vagrantfileen.

    $ vagrant init debian/bullseye64
    $ notepad Vagrantfile

Sitten koneet käyntiin ja kirjauduttiin sisään. Kokeilin kirjautua molemmille koneille ssh avulla.

        $ vagrant up
        $ vagrant ssh kone1
        $ vagrant exit
        $ vagrant ssh kone2
        
Pingattiin koneilla toisiaan, toimii!

        $ vagrant ssh kone1
        $ ping -c 192.168.88.102
        $ exit

        $ vagrant ssh kone2
        $ ping -c 1 192.168.88.101
        $ exit

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/06365af0-5754-4c5c-a3ff-08a8467460a1)

Asetetaan "kone1" masteriksi ja tarkistetaan sen IP-osoite.

    $ sudo apt-get update
    $ sudo apt-get -y install salt-master
    $ hostname -I

Asetetaan "kone2" orjaksi.

    $ sudo apt-get update
    $ sudo apt-get -y install salt-minion

Liitetään koneet yhteen lisäämällä masterin IP-osoite konfiguraatiotiedostoon ja käynnistetään orja uudelleen.

        $ sudoedit /etc/salt/minion
        $ sudo systemctl restart salt-minion.service
    
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/77779403-3935-4a0d-914a-079fcb482188)

Hyväksytään orja-avain master koneella.

        $ sudo salt-key -A

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/89657170-6045-45f8-826f-7f8621574d4d)

Asensin Apachen ja curlin ensin manuaalisesti.

    $ sudo apt-get -y install apache2
    $ sudo apt-get -y install curl

Loin /srv/salt -hakemiston, johon loin apache.sls tiedoston. Loin tilan, joka asentaa Apachen ja tarkistaa, että weppipalvelin on päällä.

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/efddda4d-02b4-4af5-9703-c16ae4ca688a)

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/ce14c453-e5df-40cd-8eae-1d3b0ec8e409)

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/35df1216-9b60-4334-be6d-b86abaa7ed64)



![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/5d9cc730-ccee-4fe4-baf5-7c2879756787)

Tällä hetkellä tila asentaa Apachen ja käynnistää sen.
![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/2324f023-f226-4275-8e2f-c32f794d2ef3)

### Tulimuuri

Lähdin asentamaan tulimuuria. Ensin manuaalisesti, sitten automatisoin asennuksen.

        $ sudo apt-get update
        $ sudo apt-get -y install ufw

Loin uuden hakemiston /srv/salt/ufw, johon loin ufw.sls -tiedoston. 
Tässä kohtasin ongelmia. Onnistuin luomaan tilan, joka asentaa ja käynnistää tulimuurin. Yritin tämän lisäksi tehdä reikää tulimuuriin. En kuitenkaan onnistunut tässä.

        ufw:
          pkg.installed

        ufw Service:
          service.running:
            - name: ufw
            - enable: True
            - require:
              - pkg: ufw

        ufw Allow:
          ufw.allow:
            - port: 22
            - proto: tcp

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/a601a386-f7f5-4c00-9081-e78310013f62)

Tässä vaiheessa luovutin portina avaamisen automatisoinnin kanssa, ja avasin portin 22 manuaalisesti, jotta pystyn jatkamaan SSH-kirjautumista

        $ sudo ufw allow 22/tcp

### Curl

Päätin luoda tilan curlin asennukselle.
Loin kansion 'curl', johon loin curl.sls -tiedoston. Lisäsin tilan tiedostoon. Lisäsin top.sls -tiedostoon curlin.

        curl:
          pkg.installed



### Git

Lähdin asentamaan Gittiä. Ensin manuaalisesti, sitten automatisoin asennuksen. 

        $ sudo apt-get update
        $ sudo apt-get -y install git
        

Loin uuden hakemiston /srv/salt/git, johon loin uuden git.sls -tiedoston. 

        git:
          pkg.installed

Lisäsin gitin top.sls -tiedostoon. 

        base:
          '*':
            - apache2.apache
            - ufw.ufw
            - curl.curl
            - git.git


## Lopputulos

![image](https://github.com/bhd471/Palvelinten-hallinta/assets/148760837/6655eb41-2a21-4858-bdf5-107dfc3b0cb9)


### Lähteet

Luettavissa: https://www.linode.com/docs/guides/configure-apache-with-salt-stack/. Luettu: 13.05.2024.

Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.firewall.html. Luettu: 13.05.2024.
