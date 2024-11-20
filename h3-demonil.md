# Demoni

## Tiivistelmät

### Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port
- Artikkeli esittelee pkg-file-service-mallin. Kyseisellä mallilla pystytään hallitsemaan palvelimia Salt-konfiguraationhallintatyökalulla.
- Mallin mukaan ohjelmisto asennetaan, konfigurointitiedosto päivitetään ja palvelu käynnistetään uudelleen, jotta uusi konfiguraatio otetaan käyttöön.
  (Karvinen, T. 2018. https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh)

### Saltin tilafunktiot: pkg, file ja service
1. Pkg
   - Tarkoituksena joko asentaa, poistaa tai päivittää paketteja.
   - Komento 'pkg.installed' varmistaa paketin asennuksen.
   - Vastaavasti 'pkg.purged' poistaa paketin.
2. File
   - Tarkoituksena hallita eri palveluiden tilaa.
   - 'file.managed' mahdollistaa tiedoston oikeanlaisen ja halutun sisällön.
   - 'file.absent' varmistaa tietyn tiedoston olevan poistettu.
   - 'file.symlink' luo symbolisen linkin.
3. Service
   - Tarkoituksena palveluiden tilan hallitseminen
   - 'service.running' huolehtii palvelun käynnissäolosta.
   - Jos halutaan varmistaa palvelun käynnissä olemattomuus, käytetään komentoa 'service.dead'.
   - 'service.enabled' varmistaa demonin uudelleenkäytettävyyden, jos pitää tehdä uudelleenkäynnistys


## Tehtävät

Kaikki tehtävänannot on löydetty kurssin tehtäväsivulta kohdasta h3-Demoni eli tämän linkin takaa: https://terokarvinen.com/palvelinten-hallinta/#h3-demoni

### a) 

Ensimmäisessä tehtävässä oli ideana asentaa Apache, korvata sen testisivu ja testata demonin toimivuus. Aloitin tehtävänteon 17.11. klo 18.15 kirjautumalla sisään master-virtuaalikoneelle. Sinne päästyäni käytin seuraavia komentoja:

    sudo apt update
    sudo apt install apache2 -y

  Kyseisillä komennoilla päivitin master-koneen paketinhallinnan ja asensin apachen. Tämä vaihe oli nopeasti ohi, joten pääsin sujuvasti jatkamaan tehtäväntekoa.

  Seuraavaksi vuorossa oli testisivun korvaaminen. Tein sen allaolevan kuvan mukaisesti:

  ![image](https://github.com/user-attachments/assets/9e2ad79b-b689-4f86-aa84-82c90af550e2)

  Tässä vaiheessa oli otollinen hetki demonin käynnistämiseen ja sen toiminnan varmistamiseen. Käytin seuraavia komentoja tässä prosessissa:

    sudo systemctl start apache2
    sudo systemctl enable apache2
    systemctl status apache2

  Sain viimeisimmän komennon jälkeen seuraavan näkymän:

  ![image](https://github.com/user-attachments/assets/a2fd2dcf-c4ff-4568-9eca-307ccdc188c0)


  Käsin tehtävien vaiheiden jälkeen siirryin luomaan pkg-file-servicea ja index.html-tiedostoa. Tein ne kuvissa näkyvillä tavoilla:

  ![image](https://github.com/user-attachments/assets/0cf37546-ec51-4db0-b1c9-a910b1ec6aa8)
  ![image](https://github.com/user-attachments/assets/522390c7-50bf-4d13-8abd-451da0645373)



  Viimeisenä vuorossa oli pkg-file-servicen ajaminen. Hoidin sen kuvan mukaisesti.

  ![image](https://github.com/user-attachments/assets/26073efa-f9c7-49da-9f4a-126ef80732f6)

  Tehtävä tuli päätökseen klo 18.50.





### b) 

Palasin takaisin tehtävien ääreen 18.11. klo 15.30. Tässä tehtävässä minun piti lisätä uusi portti, jota SSHd kuuntelee. Aloitin tehtävän tekemisen tuttuun tapaan avaamalla master-koneen. Siirryin hakemistoon /srv/salt ja syötin sinne kuvassa näkyvän komennot:

![image](https://github.com/user-attachments/assets/144161b3-2642-4342-940f-079b5b3243b3)

Olin tehnyt muokkauksia tiedostoon /etc/ssh/sshd_config. Lisäsin sinne portin 22 kaveriksi portin 1827. Tarkistin muokkausten olemassaolon cat-komennolla. Muokkauksien jälkeen uudelleenkäynnistin ssh-palvelun ja tarkistin SSHd:n kuuntelevan molemmilla asettamillani porteilla. Käytin siihen seuraavia komentoja:

    sudo systemctl restart sshd
    sudo ss -tuln | grep ssh

Tässä kohtaa tajusin, että ehkä minun pitäisi käydä päivittämässä portit myös Vagrantfileen. Ryhdyin tuumasta toiseen ja poistuin master-koneelta. Avasin host-yks-hakemistossa Vagrantfilen ja lisäsin sinne kuvanmukaisesti:

![image](https://github.com/user-attachments/assets/b09991b3-f079-4188-be57-bcfd031ff76a)

Kun Vagrantfile oli saatu ajantasalle, palasin takaisin master-koneelle ja siellä olevaan /srv/salt-hakemistoon. Päästyäni takaisin tuttuun ja turvalliseen ympäristöön, aloin pohdiskelemaan service-watchia. En löytänyt googlettelulla vastauksia, joten päätin kysyä ChatGPT:lta. Se antoi seuraavan vastauksen:

![image](https://github.com/user-attachments/assets/f7cee1b4-2c16-4a57-bb1b-4a8324d145f3)

ChatGPT:n antaman vastauksen perusteella päätin lähestyä tehtävää inotify-toolsin avulla. Syötin siis seuraavat komennot:

     sudo apt update
     sudo apt install inotify-tools

Tämän jälkeen minun piti jollain ilveellä luoda tiedosto/palvelu, joka seuraisi sshd_config-tiedostoa. Käännyin jälleen vanhan ystäväni ChatGPT:n puoleen. Se neuvoi tekemään seuraavan tiedoston:

![image](https://github.com/user-attachments/assets/e8dd1109-326a-49e0-917d-a9e6507174a7)

Tästä eteenpäin selviydyin itsenäisesti. Tehtävän viimeistelyä varten syötin seuraavat komennot:

      sudo systemctl daemon-reload
      sudo systemctl enable sshd-watch.service
      sudo systemctl start sshd-watch.service

Tehtävä tuli valmiiksi klo 16.06.


### c)

Ajattelin tehdä oman moduulini palomuurin konfigurointityökalusta. Ideana olisi yksinkertaistaa ja helpottaa ufw-palomuurin hallintaa. Voisin esimerkiksi lisätä suojausmallien testauksen ja lokien tarkastuksen.


### d) 

Pienen tauon jälkeen oli taas aika jatkaa tehtäviä! Olin jättänyt edellisen tehtävän jäljiltä master-koneen päälle, joten tällä kertaa ei tarvinnut tuhlata aikaa sisäänkirjautumiseen. Tosin tässä tehtävässä tällä ajansäästöllä ei ollut väliä, kun jouduin heti alkuun metsästämään ohjeita.

Löysin kaksi mielestäni hyvää ohjetta. Ensimmäiseksi tutkailin [DigitalOceanin](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-debian-11) ohjetta ja poimin sieltä käyttööni sopivia komentoja. Kun äskeinen lähde oli koluttu läpi, siirryin [Reintechin](https://reintech.io/blog/configuring-apache-virtual-hosts-debian-12) sivustolle keräämään tietoja.

Metsästysretkeni jälkeen palasin takaisin master-koneelle. Sinne päästyäni aloitin ohjeiden soveltamisen syöttämällä seuraavat komennot:

    sudo a2enmod userdir
    sudo systemctl restart apache2

Seuraavaksi loin uuden hakemiston ja sinne index.html-tiedoston.

![image](https://github.com/user-attachments/assets/082e6c57-194a-4555-a076-8f0cd9ec2b36)

Tähän asti olen muokannut tiedostoja sudo-oikeuksilla. Tässä tehtävässä pitäisi kuitenkin mahdollistaa tiedoston muokkaus ilman sudoa. Mahdollistin muokkauksen ilman sudoa seuraavilla komennoilla:

    sudo chown -R vagrant:vagrant /home/master/public_html
    sudo chmod 755 /home/master/public_html

Seuraavaksi vuorossa oli VirtualHostin luominen. Aloitin sen luomalla alla olevassa kuvassa näkyvän tiedoston.

![image](https://github.com/user-attachments/assets/7ef09496-089a-41be-84df-13098e6627d2)

Seuraavaksi syötin seuraavat komennot, jotta sain tiedoston käyttöön.

    sudo a2ensite pihlan_domain.conf
    sudo a2dissite 000-default.conf
    sudo apache2ctl configtest
    sudo systemctl restart apache2

Kun komennot olivat saaneet tehdä työtänsä, yritin avata sivun http://pihlan_domain, koska kaiken järjen mukaan sen pitäisi nyt toimia. Se ei kuitenkaan toiminut?! Yritin ratkoa ongelmaa palomuurin kautta.

![image](https://github.com/user-attachments/assets/6f6583e3-19dd-40c7-b0e3-f0e2e8dce56b)

![image](https://github.com/user-attachments/assets/84e5c820-3d4e-4df0-b501-25a48003ccc0)

![image](https://github.com/user-attachments/assets/d8e26d29-442c-441c-baa8-1d7392bc6091)

En saanut ratkottua, joten päädyin lopettamaan urakan 20.11. klo 11.23.



## Lähteet

DigitalOcean (2022). How To Install the Apache Web Server on Debian 11. Saatavilla: https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-debian-11.
Karvinen, T. (2018). Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Saatavilla: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh.
Karvinen, T. (2024). Tehtävänanto. Saatavilla: https://terokarvinen.com/palvelinten-hallinta/#h3-demoni.
Reintech (2024). Configuring Apache Virtual Hosts on Debian 12. Saatavilla: https://reintech.io/blog/configuring-apache-virtual-hosts-debian-12.
Saltin virallinen dokumentaatio. Tilafunktiot pkg, file ja service.
Komennot:

    sudo salt-call --local sys.state_doc pkg
    sudo salt-call --local sys.state_doc file
    sudo salt-call --local sys.state_doc service
