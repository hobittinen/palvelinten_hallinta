# h1 Tehtävät

x)

a) Tehty.

b) Tässä tehtävässä asensin Saltin virtuaalikoneeseeni. Käytin ohjeina kahta Tero Karvisen laatimaa verkkosivua. Ensimmäinen käyttämäni verkkosivu oli Palvelinten Hallinta (Karvinen 2024) ja sieltä erityisesti alaotsikon Saltin asennus alta löytyvää tietolaatikkoa. Toisena lähteenäni oli Run Salt Command Locally (Karvinen 2021).
Aloitin Saltin asentamisen avaamalla virtuaalikoneeni. Kirjauduin omilla tiedoillani koneelle, jonka jälkeen avasin terminalin. Ensimmäisenä syötin komennon sudo mkdir -p /etc/apt/keyrings. Kyseisellä komennolla tein uuden hakemiston /etc/apt/keyrings ja sille tarvittavat päähakemistot.
Kun hakemisto oli saatu aikaiseksi, siirryin seuraavan komennon pariin. Syötin komennon sudo curl -fsSL -o /etc/apt/keyrings/salt-archive-keyring-2023.gpg https://repo.saltproject.io/salt/py3/debian/12/amd64/SALT-PROJECT-GPG-PUBKEY-2023.gpg. Kyseisellä komennolla latasin GPG-avaimen Salt Projectiin. Samalla tallensin sen aikaisemmin luomaani hakemistoon.
Jäljellä oli enää viimeiset vaiheet. Toiseksi viimeinen vaihe oli komennon echo "deb [signed-by=/etc/apt/keyrings/salt-archive-keyring-2023.gpg arch=amd64] https://repo.saltproject.io/salt/py3/debian/12/amd64/latest bookworm main" | sudo tee /etc/apt/sources.list.d/salt.list. syöttäminen. Komennolla lisäsin Salt Projectin koneen APT-lähteisiin eli pystyn asentamaan ja hallitsemaan Salt-paketteja.
Viimeinkin oli viimeisten komentojen vuoro. Viimeisillä komennoilla asensin salt-minionin. Käytin seuraavia komentoja: sudo apt-get update ja sudo apt-get -y install salt-minion. Tarkistin komentojen toimivuuden komennolla sudo salt-call --version.

c) Kokeilin viittä tärkeintä Saltin tilafunktiota. Aloitin pkg:stä. Ensin minun piti syöttää komento 



# Lähdeluettelo
https://terokarvinen.com/palvelinten-hallinta/
https://terokarvinen.com/2021/salt-run-command-locally/
