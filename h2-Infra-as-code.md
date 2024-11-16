# Infra as code

x) Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant:

    - Tärkein komento on sudo apt-get update.
    - Vagrantfilen tulee sisältää KAIKKI tarpeellinen tieto, muuten ei mistään tule mitään.
    - Hostiin pääsee kirjautumaan komennolla vagrant ssh (host).
   Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux
   
    - Master asennetaan komennolla sudo apt-get -y install salt-master.
    - Slave asennetaan komennolla sudo apt-get -y install salt-minion.
    - Slaven /etc/salt/minion-tiedostoon pitää laittaa masterin ip-osoite.
    - Slaven lähettämä avain tulee hyväksyä masterilla.
   Karvinen 2014: Hello Salt Infra-as-Code
   
    - Tärkeä komento on sudoedit init.sls.
    - Testauksessa voidaan käyttää seuraavaa komentoa: sudo salt-call --local state.apply hello.
    - Idempotenttiutta testatessa voidaan käyttää komentoa sudo salt-call --local state.apply hello.
   Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves
   
    - Kun syöttää seuraavan komentosarjan, tulee muistaa oikeat sisennykset, jotta homma toimii.
    cat /srv/salt/hello/init.sls
     /tmp/infra-as-code:
     file.managed
     - Kun tiedosto on top.sls, se määrittää mitkä asiat suoritetaan millekin orjalle.
   Salt overview:
   
    - Usein oletusrenderöijä on YAML.
    - YAML-tiedot järjestetään key: value-pareihin.
    - YAML organisoidaan lohkoiksi.
    - Sisennys määrittää kontekstin.
    

a) Tässä tehtävässä tarkoituksenani oli osoittaa Vagrantin asennus omalle virtuaalikoneelleni. Aloitin tehtävän teon 8.11. asentamalla Vagrantin. VirtualBoxin olin asentanut jo aikaisemmin, joten sitä minun ei nyt tarvinnut tehdä. Kun aloitin tehtävän tekoa, oli kello 15.40. Kirjauduin sisään virtuaalikoneelleni. Jotta sain Vagrant-asennukseni alkuun, suuntasin Vagrantin viralliselle asennusohjesivulle (Vagrant). Tosin heti kun aukaisin kyseisen verkkosivun, se ohjeisti minut avaamaan toisen verkkosivun. Tottelin ohjeistusta ja avasin Vagrantin virallisen asennussivun (Vagrant), josta valitsin Linuxille sopivan paketin ladattavaksi. Paketin latauksessa kului noin 20 sekuntia. Kun paketti oli onnistuneesti latautunut, palasin asennusohjesivulle. Luin sen nopeasti läpi, minkä jälkeen siirryin virtuaalikoneelleni.

Päätin tässä välissä päivittää järjestelmäni. Käytin päivittämiseen komentoja sudo apt update ja sudo apt updgrade. Komentojen syöttämisen jälkeen päätin varmuuden vuoksi tarkistaa VirtualBoxini tilan. Tarkistusta varten käytin komentoa virtualbox --help. Komentoa seurasi haluttu tulos, joten pääsin siirtymään eteenpäin. Käytin varmuuden vuoksi komentoa sudo apt install vagrant, jotta Vagrant varmasti latautuisi. Tämän jälkeen tarkistin asennuksen onnistumisen ja Vagrantin version komennolla vagrant --version. Tässä kohtaa kello oli jo 16.05. Aikaa oli luonnollisesti mennyt Vagrantin asennuksen lisäksi myös sopivan opiskelumusiikin valitsemiseen.

![vagrant](https://github.com/user-attachments/assets/d2dab1dc-c6fc-43fa-b713-96a9e9aca31b)



b) Aikaisemmassa tehtävässä koetun ilon ja riemun takia päätin jatkaa tehtävien tekoa vielä saman päivän aikana. Aloin tekemään tätä tehtävää 8.11. klo 18.20. Hain apua tehtävän tekemiseen Tero Karvisen verkkosivulta Two Machine Virtual Network With Debian 11 Bullseye and Vagrant (Karvinen 2021). Kun avut oli metsästetty, pääsi itse tehtävän teko vauhtiin! Ensitöikseni kirjauduin takaisin virtuaalikoneelleni. Kirjautumisen jälkeen siirryin terminaaliin. Ensimmäisenä syötin sinne komennon mkdir host-yks, jolla loin hakemiston host-yks. Tämän jälkeen siirryin kyseiseen hakemistoon komennolla cd host-yks. Tässä kohtaa en enää ymmärtänyt kunnolla Karvisen sivulta löytyviä ohjeita, joten päätin etsiä apua internetistä. Kello oli tässä vaiheessa noin 18.28. Noin kymmentä minuuttia myöhemmin löysin freecodecamp-sivustolta Ijeoma Etin kirjoittaman artikkelin How to Create and Manage Virtual Machines with the Vagrant Command Line Tool (Eti 2023). Kyseisestä artikkelista otin oppia Vagrantfileen liittyen, jotta pääsisin tehtävässä eteenpäin. Sovelsin artikkelista löytynyttä komentoa vagrant init debian/bookworm64, jotta sain luotua Vagrantfilen. Tarkastin onnistumiseni Vagrantfilen luonnissa käyttämällä komentoa ls Vagrantfile.

![vagrantfile](https://github.com/user-attachments/assets/442c288a-85f7-4033-bd17-761804e65ccc)


Seuraavaksi kurkistin Vagrantfilen sisuksiin. Jotta pääsin kurkkausreissulleni, syötin terminaaliin komennon nano Vagrantfile. Allaolevasta kuvasta näkyy osa Vagrantfilen sisällöstä.

![vagrantfilensisus](https://github.com/user-attachments/assets/23bbcb9b-6607-40df-aeb9-fc489b82bd5d)


Viimeisenä, muttei vähäisimpänä oli vuorossa Vagrantfilen tallennus. Olisi harmi, jos se katoaisi bittiavaruuteen ja kova työni menisi sitä kautta hukkaan. Tallensin Vagrantfilen komennolla vagrant up. Kello oli tässä kohtaa 18.47.



c) Palasin tehtävien tekoon 9.11. klo 17.26. Ensitöikseni etsin tietoa, miten tämä tehtävä pitäisi tehdä. Tehtävän ideana oli tehdä kahden Linux-koneen verkko Vagrantilla. Löysin Tero Karvisen verkkosivuilta sivun nimeltään Two Machine Virtual Network With Debian 1 Bullseye and Vagrant (Karvinen 2021), jota käytin apuna myös aikaisemmassa tehtävässä. Kun apua tehtävän tekemiseen oli löytynyt, oli aika siirtyä virtuaalikoneelle. Tuttuun tapaan kirjauduin sisään koneelle ja siirryin terminaaliin. Terminaalissa syötin komennon cd host-yks, jotta pääsin aikaisemmassa tehtävässä luomaani hakemistoon. Päästyäni hakemistoon käytin komentoa nano Vagrantfile, jotta saisin muokattua Vagrantfilen sisältöä. Muokkasin Vagrantfilen sisällön itselleni järkeenkäyväksi ja tein sinne kaksi Linux-konetta, jonka jälkeen tallensin työnjälkeni ja poistuin nanosta. Kello oli tässä kohtaa 17.40.

Kun Vagrantfile oli saatu kuntoon, oli aika käynnistää äsken luomani koneet. Käynnistin ne komennolla vagrant up. Tämän onnistuttua heti ensimmäisellä yrityksellä pääsin jatkamaan tehtävässä eteenpäin. Seuraavaksi vuorossa oli pingaamisen osoittaminen. Tätä varten minun piti selvittää molempien koneiden IP-osoitteet. Tässä kohtaa käytin komentoa man vagrant, jotta saisin vähän vihiä siitä, miten IP-osoitteet selvitettäisiin. Onnekseni man-listasta löytyi ssh-komento, jota luonnollisesti päätin soveltaa. Syötin komennot vagrant ssh node1 -c "hostname -I" ja vagrant ssh node2 -c "hostname -I".

![osoitteet](https://github.com/user-attachments/assets/73b582ac-39fc-4608-9be8-f00f21064baa)

Nyt oli vuorossa itse pingaaminen. Tässä vaiheessa kello oli 17.50. Päätin pingata itselleni loogisessa järjestyksessä eli pingasin ensin node2. Aloitin urakan kirjautumalla node1-koneeseen komennolla vagrant ssh node1. - Kun sain kirjauduttua sisään, syötin komennon

     - ping -c 1 192.168.56.5.

Tämän jälkeen poistuin node1-koneelta ja siirryin node2-koneelle komennolla vagrant ssh node2. Pingasin node1:n komennolla ping -c 1 192.168.56.4. Pingauksen jälkeen poistuin node2-koneelta. Kello oli nyt 18.05.

![ping1](https://github.com/user-attachments/assets/4cb3690b-2d74-46d2-befc-3c17f2a25177)

![ping2](https://github.com/user-attachments/assets/fe51196f-bb94-43e7-bd30-1ed7887555de)



d) Oli aika tulla takaisin tehtävien ääreen 10.11. klo 14.26. Kävin tarkastamassa kurssin tehtäväsivulta Palvelinten Hallinta - Configuration Management Systems course - 2024 autumn (Karvinen 2024) mitä tässä tehtävässä kuuluisi tehdä. Sivulta sain selville, että nyt oli vuorossa herra-orja-demonstrointia. Aloitin tehtävänteon kirjautumalla virtuaalikoneelleni. Päästyäni sisälle koneeseen, siirryin terminaaliin ja syötin komennon cd host-yks, jotta pääsisin host-yks-hakemistoon. Kyseisessä hakemistossa sijaitsee kaikki Vagrant-juttuni. Ensimmäinen asia, minkä tein host-yks-hakemistossa oli eilen luomieni virtuaalikoneiden käynnistys. Käytin käynnistykseen komentoa vagrant up.
Koneiden käynnistyttyä siirryin node1-koneelle, jolle halusin asentaa salt-masterin. Siirtymiseen käytin komentoa vagrant ssh node1. Ennen masterin asennusta päivitin node1:n varmuuden vuoksi komennolla sudo apt-get update. Päivityksen jälkeen syötin komennon sudo apt-get install salt-master. Eipä komento toiminut. Yritin ratkoa tilannetta toistamalla komentoja sudo mkdir -p /etc/apt/keyrings ja sudo curl -fsSL -o /etc/apt/keyrings/salt-archive-keyring-2023.gpg https://repo.saltproject.io/salt/py3/debian/12/amd64/SALT-PROJECT-GPG-PUBKEY-2023.gpg. Käytin myös komentoa echo "deb [signed-by=/etc/apt/keyrings/salt-archive-keyring-2023.gpg arch=amd64] https://repo.saltproject.io/salt/py3/debian/12/amd64/latest bookworm main" | sudo tee /etc/apt/sources.list.d/salt.list. Mikään ei auttanut, joten eipä tässä mitään. Yritin toistaa seuraavien kolmen päivän aikana kaikki mahdolliset kikat (= toistin äskeisiä koodeja), mutta eipä mistään tullut mitään.

![epäonnistuminen1](https://github.com/user-attachments/assets/d3085b22-cf4e-4c3f-9215-55de7320225c)

Palasin tehtävän pariin 15.11. klo 13. Heti alkuun päätin poistaa Vagrantfilen komennolla rm Vagrantfile. Tämän jälkeen loin tiedoston uudelleen:

![image](https://github.com/user-attachments/assets/271fbecd-472d-4000-a039-94b12e843214)

Oli aika luoda itse virtuaalikone uudelleen. Sen luomisen jälkeen loin yhteyden siihen. Tosin heti yhteyden muodostamisen jälkeen poistuin virtuaalikoneesta ja tuhosin sen.

![image](https://github.com/user-attachments/assets/a4bd548f-c439-46a1-a619-b9fa67ee7a30)
![image](https://github.com/user-attachments/assets/079642b6-fa99-4049-ad9f-c0730566fcba)

Tässä kohtaa kello oli mennyt seitsemän minuuttia eteenpäin eli se oli 13.07. Tässä kohtaa muokkasin Vagrantfileä. Muokkauksen jälkeen käytin komentoa vagrant up, jolla sain luotua master- ja minion-koneet. Varmuuden vuoksi kokeilin pingaamista koneiden välillä. Onnekseni onnistuin pingauksessa. Kello oli tässä vaiheessa 13.47. Päätin pitää tauon.

![image](https://github.com/user-attachments/assets/4fc3187c-2900-4334-a0dc-04cd73168c7b)
![image](https://github.com/user-attachments/assets/55e4ab7b-fb0f-4b12-ac7b-06dd48866d78)
![image](https://github.com/user-attachments/assets/d21ef545-f87d-4a2b-808c-ed9ac5e54464)


Palasin tauoltani klo 17.00. Tällä istunnolla hoitaisin tämän tehtävän oikean tehtävän eli herraorjan kuntoon.

Aloitin tutkimalla vaihtoehtoista tapaa tehdä herraorja. Etsintöjen aikana päädyin Saltin asennusohjeisiin ja kas kummaa, sieltä löytyi hyvältä vaikuttava ohjeistus! Tämän ohjeen etsimiseen minulta oli mennyt 10 minuuttia.

Siirryin virtuaalikoneideni pariin klo 17.12. Ensin kirjauduin master-virtuaalikoneelleni. Kirjautumisen jälkeen asensin Saltin seuraavilla komennoilla:

mkdir -p /etc/apt/keyrings
curl -fsSL https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public | sudo tee /etc/apt/keyrings/salt-archive-keyring.pgp
curl -fsSL https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources | sudo tee /etc/apt/sources.list.d/salt.sources

Kun ylläolevat komennot olivat saaneet hommansa hoidettua, asensin Salt-masterin.

![image](https://github.com/user-attachments/assets/e52b41de-601e-4ba3-9285-7d8a94ec63a4)

Salt-masterin asennuksen jälkeen vuorossa oli Salt-minionin asennus. Kirjauduin ulos master-koneelta ja kirjauduin sisälle slave-koneelle. Suoritin samat komennot kuin master-koneelle, paitsi asensin tietysti Salt-masterin sijaan Salt-minionin.

![image](https://github.com/user-attachments/assets/4b7942c6-6b2e-4d87-85a6-7367742d10ce)

Kävin vielä muokkaamassa slaven /etc/salt/minion-tiedostoa, jotta siellä oli master-kohdassa master-virtuaalikoneeni ip-osoite. Tämän jälkeen käynnistin Salt-minionin uudelleen.

![image](https://github.com/user-attachments/assets/9b0cfb2d-75ab-4282-9f01-4a979540e0f4)
![image](https://github.com/user-attachments/assets/1b010b99-9468-4f01-88d4-a74fbdc3f241)

Viimeisenä, muttei vähäisimpänä palasin takaisin master-koneeelle. Sieltä tarkastin hyväksyntää odottavat avaimet. Siellä oli hyväksyntää vailla vain slaven avain, jonka tietenkin hyväksyin. Hyväksynnän jälkeen vielä kokeilin minionin toimintaa ja luojan kiitos se toimi! Melkein viikon mittainen operaationi oli ohi!!!

![image](https://github.com/user-attachments/assets/c9b30d77-130e-45a2-8461-f82d55080e5a)

e) Aloitin tekemään tätä tehtävää 16.11. klo 13.43. Ensin kirjauduin takaisin master-koneelle, jonne loin uuden hakemiston /srv/salt/moikku. Tämän jälkeen loin init.sls-tiedoston.

![image](https://github.com/user-attachments/assets/6ad783da-b224-438f-be7c-f7e064f57ed1)
![image](https://github.com/user-attachments/assets/949aefe3-db74-4b5f-a24e-2199a1272d0c)
![image](https://github.com/user-attachments/assets/62901d76-9eee-4fab-9d7c-fec875a69bfc)


Kuten saatoit huomata, init.sls-tiedoston luonnin aikana onnistuin luomaan myös komennon, joka luo hellurei-tiedoston. Päätin testata komentoa, jotta hellurei oli varmasti luotu. Vainoharhaisuuteen taipuvaisena päätin kuitenkin vielä tarkastaa tiedoston olemassaolon alla olevan kuvan mukaisesti:

![image](https://github.com/user-attachments/assets/0bd4ba08-760c-48a3-b59d-2e9bfcba27e0)

Onnekseni kaikki oli mennyt putkeen. Pääsin lopettamaan tämän tehtävän 14.07.


f) Pidin noin tunnin mittaisen tauon edellisen tehtävän jälkeen. Palasin master-koneelle klo 15.12. Nyt oli vuorossa tiedoston ajoa orjalla. Aloitin homman varmistamalla herran ja orjan yhteyden:

![image](https://github.com/user-attachments/assets/d7d137c2-6365-4a32-a1d7-baf6f754a72d)

Jatkoin tehtäväntekoa kuvassa näkyvällä tavalla:

![image](https://github.com/user-attachments/assets/10c08f7e-d062-4536-a208-ddc693359a34)

Viimeistelin tehtävän siirtymällä master-koneelta slave-koneelle. Slaveen päästyäni tutkailin /tmp/-hakemistoa, jotta saisin varmuuden tehtävän onnistumisesta.

![image](https://github.com/user-attachments/assets/b60c5e52-a22b-4915-82ad-97fc020b6e92)

Tehtävä valmistui 15.27.


g) Laiska olento kun olen, oli pakko taas pitää tauko. Palasin tehtävien tekoon klo 17.00. Kävin tarkastamassa tehtäväsivulta, mitä tässä tehtävässä pitäisi tehdä ja sain selville, että nyt vuorossa olisi sls-tiedoston tekoa.

Aloitin etsimällä ohjeita tehtäväntekoon. Löysin sopivasti opettajan tekemät ohjeet allaolevasta osoitteesta:

     - https://terokarvinen.com/2018/apache-user-homepages-automatically-salt-package-file-service-example/?fromSearch=apache

Ohjeiden löytymisen jälkeen aloitin tehtävän kirjautumalla takaisin master-koneelle. Loin sinne moduulin /srv/salt/apache, jonne loin samantien init.sls-tiedoston. Samaan aikaan loin myös default-index.html-tiedoston.

![image](https://github.com/user-attachments/assets/98169c7a-2700-48a2-8baa-f49896c0cb7c)

![image](https://github.com/user-attachments/assets/6464e0d6-316d-4755-a96d-443cc619a4d7)

Seuraavaksi syötin ajoin moduulin ensimmäistä kertaa. Samalla asensin Apachen master-koneelle. Unohdin ottaa kuvan tästä vaiheesta. Muistin kuitenkin ottaa kuvan toisesta ajosta:

![image](https://github.com/user-attachments/assets/6f907d9e-a07d-4093-a72d-44ba6f2a2577)

Päätin tarkistaa moduulin idempotenttiuden. Siirryin master-koneelta slave-koneelle. Käytin kuvassa näkyviä komentoja todetakseni, että kaikki oli kunnossa ja tehtävä saatiin päätökseen klo 17.40.

![image](https://github.com/user-attachments/assets/288ef7d2-63a8-4144-8ca8-b6209cbdcce2)


h) Jäljellä oli viimeinen pakollinen tehtävä. Aloitin sen teon klo 17.47 uloskirjautumalla slave-koneesta ja sisäänkirjautumalla master-koneeseen. Siirryin komennolla cd /srv/salt kyseiseen hakemistoon. Loin hakemistoon top.sls-tiedoston, jonka sisällön näkee allaolevasta kuvasta.

![image](https://github.com/user-attachments/assets/eccc06c5-5825-4d35-ae79-9eabd4ef0a7b)

Käsitykseni mukaan olin onnistunut tekemään sellaisen top.sls-tiedoston, jolla pystyisi ajamaan sekä hello- että apache-moduulit. Jotta saisin täyden varmuuden työni jäljestä, käytin seuraavaa komentoa:
            
     $ sudo salt '*' state.apply

![image](https://github.com/user-attachments/assets/158bca16-57ce-474b-a367-d6fd86afaa29)

Ei onnistunut tällä kertaa. Päätin myöntyä ja tehdä erikseen hello.sls- ja apache.sls-tiedostot.

![image](https://github.com/user-attachments/assets/a8aa5d12-2595-4d44-963c-9cd0f866cb7e)

Kun kaikki sls-tiedostot oli saatu luotua, kokeilin viimeistellä tehtävän orjalla:
                
                $ sudo salt '*' state.apply

Viimeistely onnistui! Tehtävä valmistui klo 18.12. Alla on todistusaineisto.

![image](https://github.com/user-attachments/assets/b39ecd21-5025-45c8-bf35-6e4e3990bafa)
![image](https://github.com/user-attachments/assets/83b2d5f4-3068-4ea4-9348-e957f680496d)



# Lähdeluettelo

https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html

Eti, I. (2023). How to Create and Manage Virtual Machines with the Vagrant Command Line Tool. FreeCodeCamp. Saatavilla: https://www.freecodecamp.org/news/create-and-manage-virtual-machines-with-vagrant/

HashiCorp (2024). Vagrant Installation Guide. Saatavilla: https://developer.hashicorp.com/vagrant/docs/installation

Karvinen, T. (2021). Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. Saatavilla: https://www.terokarvinen.com

Karvinen, T. (2018). Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. Saatavilla: https://www.terokarvinen.com

Karvinen, T. (2014). Hello Salt Infra-as-Code. Saatavilla: https://www.terokarvinen.com

Karvinen, T. (2023). Salt Vagrant - automatically provision one master and two slaves. Saatavilla: https://www.terokarvinen.com

Salt Overview. YAML - The Configuration Language of SaltStack. Saatavilla: https://docs.saltstack.com/en/latest/topics/tutorials/yaml.html
