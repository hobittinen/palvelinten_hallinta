# Demoni

## Tiivistelmät


## Tehtävät

Kaikki tehtävänannot on löydetty kurssin tehtäväsivulta kohdasta h3-Demoni.

a) Ensimmäisessä tehtävässä oli ideana asentaa Apache, korvata sen testisivu ja testata demonin toimivuus. Aloitin tehtävänteon 17.11. klo 18.15 kirjautumalla sisään master-virtuaalikoneelle. Sinne päästyäni käytin seuraavia komentoja:

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



  b) Palasin takaisin tehtävien ääreen 18.11. klo 15.30. Tässä tehtävässä minun piti lisätä uusi portti, jota SSHd kuuntelee. Aloitin tehtävän tekemisen tuttuun tapaan avaamalla master-koneen. Siirryin hakemistoon /srv/salt ja syötin sinne kuvassa näkyvän komennot:

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








