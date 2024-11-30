# Loppuhuipennus

## a) Miniprojektin valmiiksi tekeminen

Jatkoin palomuurin konfigurointityökalun jalostamista 30.11. klo 15.23. Ensimmäiseksi päätin tarkistaa, että viime sessiossani tekemät muutokset olivat kunnossa.

![image](https://github.com/user-attachments/assets/2292c8c2-88bc-45ae-9e5d-bc0ba1cc6ad4)

Huomattuani kaiken olevan kunnossa, pystyin jatkamaan työni tekoa rauhallisin mielin. Päätin katsoa ufw:n oletuskäytännöt seuraavaa komentoa käyttäen.

    sudo grep -i '^default_' /etc/default/ufw

Komento tulosti tällaisen maiseman:

![image](https://github.com/user-attachments/assets/7e2143fd-03f5-473a-96cf-b158739f0257)

Seuraavaksi muutin muutamaa oletuskäytäntöä kuvan mukaisesti:

![image](https://github.com/user-attachments/assets/20f0fc2a-5fc7-48e1-8e31-cb964fffdb75)

Äsken siis sallin kaiken saapuvan liikenteen ja estin kaiken lähtevän liikenteen. Nyt päätin kääntää asiat toisinpäin eli estää saapuvan liikenteen ja sallia lähtevän liikenteen. Käytin seuraavia komentoja:

    sudo ufw default deny incoming
    sudo ufw default allow outgoing

Sain uuden idean: reititetty liikenne! Toteutin sen, jonka jälkeen tarkistin asetukset.

![image](https://github.com/user-attachments/assets/c7a341c4-1bc1-48db-ab86-2e317d04fc22)

Seuraava siirtoni oli suoraan [täältä](https://www.cyberciti.biz/faq/set-up-a-firewall-with-ufw-on-debian-12-linux/). Sallin kaiken liikenteen LXD-säilölle Debian Linux by lxdbr0 -käyttöliittymässä.

![image](https://github.com/user-attachments/assets/0a7885cb-3e85-4f13-b8fa-06c396128c4f)

Nyt oli vuorossa ufw-palvelun hallintaa. Käytin seuraavia komentoja hallintaan.

    sudo ufw status
    sudo ufw status verbose
    sudo ufw status numbered

Tässä välissä päätin pitää tauon. Kello oli 15.46.

Palasin tauoltani samana päivänä klo 18.25. Ensimmäinen asia, jonka tein taukoni jälkeen oli sääntöjen lisääminen. Aloitin sääntöjen lisäämisen "allow"-säännöistä.

![image](https://github.com/user-attachments/assets/3654ffe3-5c93-419e-aaa8-e42edb1318b7)
![image](https://github.com/user-attachments/assets/c2db500b-51c4-4ce7-9e5a-114bb47473dc)

"Allow"-sääntöjen jälkeen vuorossa oli "deny"- ja "reject"-säännöt. Tein ne kuvassa näkyvillä tavoilla.

![image](https://github.com/user-attachments/assets/ffb9a318-32d6-430d-94e7-550e890b9ac3)

En ollut tyytyväinen sääntöihin, joten muokkailin niitä vähän. Lopputuloksena sain aikaiseksi tällaisen taulukon:

![image](https://github.com/user-attachments/assets/c9ac4598-2baf-4bf3-ba9d-255979b91c0c)

Luulin sääntöjen kanssa sekoilun olevan ohi, mutta ei se ollutkaan. Vilkaisin ohjesivua ja totesin, ettei tänään enää jaksaisi asennella sääntöjä. Päätin lopettaa tämän päivän työt klo 18.55.
