# h4 Puolikas

## Palomuurin konfigurointi

Tässä tehtävässä aloitin moduulini teon. Kuten otsikosta näkee, moduulini aiheena oli palomuurin konfigurointi.

Ennen tehtävän aloittamista minun piti etsiä ohjeet tehtäväntekoa varten. Löysinkin sopivan ohjeen [täältä](https://www.cyberciti.biz/faq/set-up-a-firewall-with-ufw-on-debian-12-linux/)

Aloitin virallisesti tehtävän tekemisen 26.11. klo 20.56. Tehtävän teko alkoi virtuaalikoneen avaamisella. Toisin kuin aikaisemmissa tehtävissä, en siirtynyt master-koneeseen, vaan jäin "pääkoneelle". Syötin komentoriville seuraavat komennot:

    sudo apt update
    sudo apt upgrade

Kyseisillä komennoilla päivitin virtuaaalikoneeni pakettivarastot. Kun päivitykset oli saatu tehtyä, uudelleenkäynnistin virtuaalikoneen alla olevalla komennolla:

    sudo reboot

Seuraavaksi pääsin itse asiaan eli palomuuriin! Asensin sen, tarkastin sen version ja sallin ssh:n seuraavilla komennoilla:

    sudo apt install ufw
    sudo ufw version
    sudo ufw allow ssh

Ssh:n sallinta ei riittänyt minulle, joten päätin huvin vuoksi sallia myös http:n ja https:n. Tarkastin vielä porttien aukiolon.

    sudo ufw allow http
    sudo ufw allow https
    sudo ufw show added

Koska aloin tekemään tehtävää illalla, en tulisi saamaan sitä yhden istunnon aikana valmiiksi. Päätin tehdä ykköspäivänä vielä yhden vaiheen. Kyseinen vaihe oli ufw:n käyttöönotto. Suoritin sen seuraavilla komennoilla:

    sudo ufw status
    sudo ufw enable

Ykköspäiväni tuli päätökseen klo 21.08.

Seuraavana päivänä, eli 27.11., huomasin ettei minulla ollutkaan aikaa tehdä tehtävää ennen klo 14. Palautin tehtävän sillä mielin, että jatkaan sitten kunhan vain kerkiän.
