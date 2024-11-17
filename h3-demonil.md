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

  


