# Viikon 4 palautus

Viikon 4 tehtävät olivat seuraavat:

- x)[ Lukea ja tiivistää muutamien ranskalaisten viivojen avulla kaksi artikkelia liittyen pilvipalvelimiin.]()
- a)[ Vuokrata oma virtuaalipalvelin.]()
- b)[ Tehdä alkutoimet virtuaalipalvelimelle ]()
- c)[ Asentaa weppipalvelin virtuaalipalvelimelle.]()
- d)[ Vuokrata domain]()

Lisäksi alla vielä suorat linkit fyysisen koneen tietoihin sekä alkutilanteen kuvaukseen:

- [ Fyysisen koneen tiedot]()
- [ Virtuaalikoneen tiedot]()
- [ Alkutilanteen kuvaus]()

Osion lähteet: (Karvinen 2024.)

---

## Fyysinen tietokone

- Windows 11 Home
  - Versio: 23H2
- Nvidia rtx 2060 näytönohjain
  - 6 GB muistia
- Intel i7-9750H prosessori
  - 6 ydintä
- 2 x 8GB Ram
- 1000 GB NVMe m.2 SSD
  - Josta vapaana +700Gb
- Viimeisimmät päivitykset ja ajurit asennettuna 6.2.2024

---

## Virtuaalikone

Virtuaalikonetta ajetaan `Oracle VM VirtualBox 7.0.12`
Virtuaalikoneen tiedot:

- Debian 12.4.0
- 40Gb muistia
- 4Gb Ram

---

## Alku

Ennen kuin siirryin alempana olevien asennuksien, toimintojen ja tehtävien pariin, suoritin seuraavat vaiheet:

1. Käynnistin virtuaalikoneen
2. Käynnistin terminaalin vasemmasta yläreunasta painamalla `Applications` -> `Terminal Emulator`
3. Syötin terminaaliin komennon: `sudo apt-get update` ja annoin salasanan.
4. Muutaman sekunnin päästä terminaaliin tuli teksti `Reading package lists... Done`  
   ![Alku1](alku1.png)

---

## x) Pilvipalvelinartikkelit

#### Lehdon artikkelin tiivistys
- abc

## a) Pilvipalvelimen vuokraus
- abc
Aloitin homman menemällä githubin [education sivulle](https://education.github.com/pack) josta huomasin, että kun kirjaudun githubin tunnuksella DigitalOcean palveluun, saan sinne 200$ arvosta credittejä. Vahvistin sähköpostiosoitteen ja täytin maksu- ja osoitetiedot [Digital Oceanin sivuille](https://www.digitalocean.com/) ja seuraavaksi päästään itse pilvipalvelimen vuokraukseen ja asennukseen.

1. Kirjauduttuani sisään, valitsin `Deploy a virtual machine`  
  ![Kuva a1](a1.png)  

2. Seuraavaksi valitsin, mistä maasta haluan palvelimen vuokrata ja tässä tapauksessa valitsin `Amsterdamin`, koska se oli lähimpänä omaa sijaintiani.

3. Seuraava osio, mitä muutin oli käyttöjärjestelmän valintaosio, missä valitsin `Debian` ja versioksi `12 x64`

4. `CPU Options` osion valinnat: 
    ![Kuva a2](a2.png)  

5. Seuraavaksi lisättiin Rootin salasana(HUOM! Salasanan tulee olla erittäin vahva!)

6. Seuraavaksi vaihdettiin Hostname osioon nimi jonka jälkeen painetaan `Create Droplet`
    ![Kuva a3](a3.png)  

7. Sivusto vaihtui ja muutaman sekuntin ajan virtuaalipalvelinta rakennettiin, jonka jälkeen painetaan virtuaalipalvelimen nimeä ja otetaan talteen ipv4 osoite.

## b) Virtuaalipalvelimen alkutoimet

##### SSH etäyhteyden muodostaminen 
1. Avataan virtuaalikoneen debian ja terminaali.
2. Ensimmäiseksi kirjaudutaan sisään Root käyttäjänä aikaisemmin tehdylle palvelimelle ssh komennolla `ssh root@IP` jossa IP on edellisen osion viimeisessä vaiheessa talteen otettu ipv4 osoite.

3. Sain virheen, joten arvelin, että ssh pitää asentaa.
    >bash: ssh: command not found

4.  Googlen avulla sain asennus ohjeet ja kirjoitin seuraavat komennot. (Gite 2023.)
    > sudo apt-get update
    > sudo apt-get install openssh-server
    > sudo systemctl start ssh

5. Uusi kirjautumis yritys komennolla `ssh root@178.128.246.214` joka onnistui:
  ![kuva d1](d1.png)

Osion lähteet: (Karvinen 2017, Gite 2023.)


##### Palomuuri 
Kun SSH yhteys saatiin muodostettua, oli aika laittaa palomuuri päälle.

1. Ohjeistuksen mukaan ensimmäisenä tein palomuuriin reiän komennolla: `sudo ufw allow 22/tcp`, mutta sieltä tuli alla oleva virhe, joka johtuu siitä, ettei sitä ollut asennettu.
    >sudo: ufw: command not found
2. Palomuurin asennus on ohi muutamassa sekunnissa, jonka jälkeen tein aikaisemmin yritetyn reiän palomuuriin ja lopuksi palomuuri päälle:
    >sudo apt-get install ufw 
    >sudo ufw allow 22/tcp
    >sudo ufw enable  
  ![kuva d2](d2.png)

Osion lähteet: (Karvinen 2017)

##### Root-tunnus kiinni
Seuraavaksi tein uuden käyttäjän jonka jälkeen suljin root-tunnuksen.

1. Komennolla `sudo adduser nicklas` tein tunnuksen, jonka jälkeen syötin tunnukselle **vahva** salasanan.(Muita tietoja ei tarvita)
2. Komennolla `sudo adduser nicklas sudo` lisäsin tunnukseen sudo oikeidet. Tässä kohtaa huomasin jonkinlaisen perl: warning: osion, joka täytyy myöhemmin selvittää.
  ![kuva d3](d3.png)
3. Kokeilin juuri luodulla tunnuksella kirjautumista toisessa terminaalissa. `ssh nicklas@178.128.246.214`
    ![kuva d4](d4.png)
4. Testasin tunnuksen sudo-oikeuksien toiminnan ajamalla alla olevat:
  >sudo apt-get update
  >sudo apt-get -y dist-upgrade
  
  Nämä komennot toivat uusia tuttavuuksia, joille en tehnyt mitään, koska hommat toimivat. Pitää myös tästä kysyä myöhemmin opettajalta.
  ![kuva d5](d5.png)
  ![kuva d6](d6.png)
  
5. Kun luodun tunnuksen sudo oikeudet on varmistettu, lukitsin rootin:
    > sudo usermod --lock root

6. Lisäksi disabloin SSH root login mahdollisuuden:
    > sudoedit /etc/ssh/sshd_config

    Avautuneessa tiedostossa vaihdoin alla olevan osion ja tallensin.
    >  PermitRootLogin  **no**

    SSH restart viimeisenä vaiheena.
    > sudo service ssh restart

7. Suljin terminaalin ja yritin kirjautua rootilla:
   ![kuva d7](d7.png)

Osion lähteet: (Karvinen 2017)

## c) Kotisivut palvelimelle
- abc
## d) Palvelimen ohjelmien päivitys
- abc

## Karvisen artikkelin tiivistys

Osion lähteet: (Lehto 2022, Karvinen 2017.)

---



## b) Virtuaalipalvelimen alkutoimet

Osio sisältää seuraavat toimet: Tulimuuri päälle, root-tunnus kiinni sekä ohjelmien päivitys.

Osion lähteet: ()

---

## c) Weppipalvelimen asennus virtuaalipalvelimelle

Tässä osiossa asennetaan weppipalvelin aiemmin hankitulle virtuaalipalvelimelle, korvataan vakiona oleva testisivu ja testataan myös, että sivu näkyy julkisesti.

Osion lähteet: ()

---

## d) Domainin vuokraus

Vuokrasin domainin [Namecheapin](www.namecheap.com) kautta heti tunnin jälkeen, koska sieltä sattui löytymään omalle sukunimelle .com päätteinen domain. Tässä osiossa käydään siis vain asetukset läpi, eikä itse domainin ostoon liittyviä toimenpiteitä.

Osion lähteet: ()

---

## Lähteet

Karvinen, T. 2017. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. Luettavissa: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/. Luettu: 6.2.2024.

Karvinen, T. 2024. Linux Palvelimet 2024 alkukevät. Luettavissa: https://terokarvinen.com/2024/linux-palvelimet-2024-alkukevat/. Luettu: 6.2.2024.

Lehto, S. 2022. Teoriasta käytäntöön pilvipalvelimen avulla (h4). Luettavissa: https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/. Luettu: 6.2.2024.



Gite, V. 2023. Ubuntu Linux install OpenSSH server. Luettavissa: https://www.cyberciti.biz/faq/ubuntu-linux-install-openssh-server/. Luettu: 6.2.2024.