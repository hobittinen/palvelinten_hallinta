# moikkuu

x)

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

Nyt oli vuorossa itse pingaaminen. Tässä vaiheessa kello oli 17.50. Päätin pingata itselleni loogisessa järjestyksessä eli pingasin ensin node2. Aloitin urakan kirjautumalla node1-koneeseen komennolla vagrant ssh node1. Kun sain kirjauduttua sisään, syötin komennon ping -c 1 192.168.56.5. Tämän jälkeen poistuin node1-koneelta ja siirryin node2-koneelle komennolla vagrant ssh node2. Pingasin node1:n komennolla ping -c 1 192.168.56.4. Pingauksen jälkeen poistuin node2-koneelta. Kello oli nyt 18.05.

![ping1](https://github.com/user-attachments/assets/4cb3690b-2d74-46d2-befc-3c17f2a25177)

![ping2](https://github.com/user-attachments/assets/fe51196f-bb94-43e7-bd30-1ed7887555de)
