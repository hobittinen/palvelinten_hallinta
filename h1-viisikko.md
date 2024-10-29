# h1 Tehtävät

x) Käytin tiivistyksessä lähteinä Tero Karvisen nettisivuja Run Salt Command Locally (Karvinen 2023), Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux (Karvinen 2018) ja Raportin kirjoittaminen (Karvinen 2006).
- Sudo apt-get update on erittäin hyödyllinen komento ja sitä tarvitaan usein.
- Raporttien tulee olla täsmällisiä ja selkeitä.
- Saltissa käytetään funktiossa usein "salt-call".

a) Tehty.

b) Tässä tehtävässä asensin Saltin virtuaalikoneeseeni. Käytin ohjeina kahta Tero Karvisen laatimaa verkkosivua. Ensimmäinen käyttämäni verkkosivu oli Palvelinten Hallinta (Karvinen 2024) ja sieltä erityisesti alaotsikon Saltin asennus alta löytyvää tietolaatikkoa. Toisena lähteenäni oli Run Salt Command Locally (Karvinen 2023).
Aloitin Saltin asentamisen avaamalla virtuaalikoneeni. Kirjauduin omilla tiedoillani koneelle, jonka jälkeen avasin terminalin. Ensimmäisenä syötin komennon sudo mkdir -p /etc/apt/keyrings. Kyseisellä komennolla tein uuden hakemiston /etc/apt/keyrings ja sille tarvittavat päähakemistot.
Kun hakemisto oli saatu aikaiseksi, siirryin seuraavan komennon pariin. Syötin komennon sudo curl -fsSL -o /etc/apt/keyrings/salt-archive-keyring-2023.gpg https://repo.saltproject.io/salt/py3/debian/12/amd64/SALT-PROJECT-GPG-PUBKEY-2023.gpg. Kyseisellä komennolla latasin GPG-avaimen Salt Projectiin. Samalla tallensin sen aikaisemmin luomaani hakemistoon.
Jäljellä oli enää viimeiset vaiheet. Toiseksi viimeinen vaihe oli komennon echo "deb [signed-by=/etc/apt/keyrings/salt-archive-keyring-2023.gpg arch=amd64] https://repo.saltproject.io/salt/py3/debian/12/amd64/latest bookworm main" | sudo tee /etc/apt/sources.list.d/salt.list. syöttäminen. Komennolla lisäsin Salt Projectin koneen APT-lähteisiin eli pystyn asentamaan ja hallitsemaan Salt-paketteja.
Viimeinkin oli viimeisten komentojen vuoro. Viimeisillä komennoilla asensin salt-minionin. Käytin seuraavia komentoja: sudo apt-get update ja sudo apt-get -y install salt-minion. Tarkistin komentojen toimivuuden komennolla sudo salt-call --version.

c) Kokeilin viittä tärkeintä Saltin tilafunktiota. Kokeiluja varten katsoin neuvoja Tero Karvisen verkkosivulta Run Salt Command Locally (Karvinen 2023). Aloitin pkg:stä eli packagesta. Syötin komentoriville aiemmin mainitsemaltani sivulta löytyneen komennon sudo salt-call --local -l info state.single pkg.installed tree. Kyseisellä komennolla asensin "tree"-paketin virtuaalikoneelleni. Päätin kokeilla toistakin sivulta löytyvää komentoa. Kyseinen komento oli sudo salt-call --local -l info state.single pkg.removed tree. Tällä komennolla onnistuin poistamaan äsken asentamani "tree"-paketin.
Seuraavaksi vuorossa oli file-funktiot. Valitsin ensimmäiseksi kokeiluun komennon sudo salt-call --local -l info state.single file.managed /tmp/hellopihla. Tällä komennolla pystyn hallitsemaan tiedostoa, joka sijaitsee osoitteessa /tmp/hellopihla. En kuitenkaan pystynyt määrittämään tiedoston ominaisuuksia äsken käyttämälläni komennolla. Seuraavaksi lähdin kokeilemaan, mitä saisin aikaiseksi komennolla sudo salt-call --local -l info state.single file.managed /tmp/moikkupihla contents="foo". Huomasin saaneeni aikaan sen, että /tmp/moikkupihla-osoitteessa sijaitseva tiedosto sisältää tekstin "foo". Viimeisenä, mutta ei vähäisimpänä päätin testata komentoa sudo salt-call --local -l info state.single file.absent /tmp/hellopihla. Tämä komento poistaisi tiedoston /tmp/hellopihla-polusta, jos siellä olisi tiedosto.
Kun file-funktiot oli saatu taputeltua, siirryin seuraavien haasteiden pariin. Päätin pureutua serviceen liittyviin komentoihin. Aloituskomentonani oli sudo salt-call --local -l info state.single service.running apache2 enable=True. Tosin komento ei toiminut, koska minulla ei ollut apache2 asennettuna virtuaalikoneelleni. Yritin asentaa apache2 koneelleni käyttämällä komentoja apache2 -v ja sudo salt-call --local -l info state.single file.managed /srv/salt/apache.sls. Kumpikaan ei toiminut, joten jäin jumiin.
![apache](https://github.com/user-attachments/assets/f4ccc693-0824-4a02-97ec-d1d4f8617a6a)

En saanut ratkaistua service-ongelmia, joten siirryin eteenpäin. Otin kohteekseni useriin liittyvät komennot. Loin uuden käyttäjän, pihlahobitin, syöttämällä komentoriville komennon sudo salt-call --local -l info state.single user.present pihlahobitti. Vastaavasti käyttämällä komentoa sudo salt-call --local -l info state.single user.absent pihlahobitti, poistin pihlahobitin. Palautin hänet myöhemmin takaisin, koska tykästyin hänen nimeensä.
Viimeisenä viidestä tärkeimmästä tilafunktiosta oli cmd. Kokeilin sitä käyttämällä komentoa sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo". Tällä komennnolla sain luotua tyhjän tiedoston nimeltään /tmp/foo.

d) Tässä tehtävässä annan esimerkin idempotentista. Aivan ensimmäisenä loin tiedoston nimeltä kontu.sls osoitteeseen /srv/salt. Tein tämän käyttämällä seuraavia komentoja: sudo mkdir -p /srv/salt ja echo "kontu:\n  pkg.installed:\n - name: kontu" | sudo tee /srv/salt/kontu.sls. Seuraavaksi käytin komentoa sudo nano /srv/salt/kontu.sls. Kirjoitin tiedostoon haluamani asiat ja tallensin sen. Tarkistin onnistumiseni syöttämällä komennon sudo salt-call --local state.apply kontu. Idempotentti ilmenee siten, että komentojen tulos on aina sama.

e) Kokeilin herra-orja arkkitehtuuria siten, että molemmat ovat samalla koneella. Aloitin prosessin tutustumalla Tero Karvisen verkkosivuun Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux (Karvinen 2018). Ensimmäiseksi latasin herran. Käytin ensiksi komentoa sudo apt-get update, jonka jälkeen komentona oli sudo apt-get -y install salt-master. Viimeistelin herran lataamisen komennolla hostname -I. Seuraavaksi loin orjan. Käytin orjan luomiseen seuraavia komentoja järjestyksessä: sudo apt-get update, sudo apt-get -y install salt-minion ja sudoedit /etc/salt/minion. Viimeiseksi käytin komentoa sudo systemctl restart salt-minion.service.
Nyt vuorossa oli orja-avaimen hyväksyttäminen herralle. Syötin komentoriville komennon salt-key -A. Vastoin odotuksia se ei toiminut. Yritin korjata tilannetta käyttämällä muun muassa seuraavia komentoja: sudo systemctl restart salt-minion, sudo cat /var/log/salt/minion ja sudo systemctl status salt-minion. Mikään ei auttanut.
![avain](https://github.com/user-attachments/assets/0b64f9fe-615c-401b-8e4c-b6b66fddf42d)


# Lähdeluettelo
https://terokarvinen.com/palvelinten-hallinta/

https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/

https://terokarvinen.com/2021/salt-run-command-locally/

https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/
