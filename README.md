# Linux Palvelimet 2024 alkukevät - kurssin materiaalit/tehtävät


https://terokarvinen.com/


Hyödyllisiä komentoja muistikatkosten varalle:
`sudo apt-get update` Pitää ajaa ennen asennuksia  
`sudo apt-get install` Lataa ohjelmia  
`cd`  
`cd ..`  
`mkdir kansio/` Luo kansio  
`mkdir -p /home/nicklashh/kansio1/toinenkansio` Luo 2 kansiota sisäkkäin  
`mv vanha uusi` Kansion uudelleen nimeäminen  
`cp alkup uusi` Kopio  
`cp -r alkup uusi` kansion kopioi  
`sudo cp kansio /usr/local/bin/` Kopioi kansion "kansio" polkuun /usr/local/bin/  
`rm poistettava` Poistaminen  
`rm -r kansionimi` Poistaa alikansiot kaiken  
`rmdir` kansion poisto  
  
`find` Näyttää kaiken sisällön  
`pwd` Näyttää hakemiston  
`ls` Näyttää tiedostot  
`whoami`  

`sudo chmod ugo+rx kansio` Antaa oikeuder read ja execute kansiolle kansio (user, group, others)  

`man ohjelmanNimi` manuaali  
`-i` ei väliä onko iso vai pieni kirjain  
`nl` Rivinumerointi  
`sudo ls /var/log/apache2/`  

`ls -d hakemisto` Näytä hakemiston tiedot  

`sudo apt-get update`  
`sudo apt-get -y install micro bash-completion`  
`export EDITOR=micro`  
`editor=micro`  

`sudo tail -f /var/log/apache2/access.log`  
`sudo tail -1 /var/log/apache2/access.log`  
`sudo tail /var/log/apache2/error.log`  

`ls -l /home/nicklashh` näyttää oikeuksia  
`ls -F | less`  
`ls -Fd sites-*` Näyttää kansiot jokerimerkillä  
`ls l sites-enabled` näyttää sisällön  

---

> mkdir viikonpaivat  
> cd viikonpaivat  
> ls  
> mkdir ma  
> cd ma/  
> touch kissa.txt  
> touch koira.md  
  
> cd ..  
> pwd  
> ls  

> cp -r ma/ ti  
> cp -r ma/ ke  
> cp -r ma/ to  
> cp -r ma/ pe  
> cp -r ma/ la  
> cp -r ma/ su  

---

##### Micro

micro editor automaagisesti  
kotihakemisto  
`ls -a`  
`export PS1='\W\$ '`  
`export EDITOR='micro'`  

`cd /etc micro bash.bashrc` export EDITOR='micro' (Viimeiselle riville)  

---

##### Apache

`/home/nicklashh/publicsites`  
`mkdir paita.example.com`  
`micro paita.example.com/index.html`  
`sudoedit /etc/apache2/sites-available/paita.example.com.conf`  
`sudo a2ensite paita.example.com`  
`sudo systemctl restart apache2`  
`sudoedit /etc/hosts`  
  
---

`history` Näyttää historian  
`history | less` Näyttää selkeemmin  

---

##### kellonaika

`timedatectl`  
`sudo timedatectl set-time "2024-02-13 tunnit:minuutit"`  
  
---

Jos host ei toimi  
`sudo apt-get update`  
`sudo apt-get install bind9-host`  

---

##### Oikeuksista

oikeuksien tarkistus: ls -l (sen hakemiston yläpuolella mistä halutaan tarkistaa)  
`chown kayttaja:ryhma`  
`sudo chown nicklashh:nicklashh`  
  
---

##### skriptejä

`#!/bin/bash`  
`sudo cp hello.py /usr/local/bin/`    
`sudo chmod ugo+rx hello.py`  
`sudo cp wpl /usr/local/bin/`<-- alkup kansiossa  
`sudo chmod ugo+rx wpl`<-- alkup kansiossa  

---

##### DJANGO

`sudo apt-get update`  
`sudo apt-get -y install virtualenv`  
`mkdir django`  
`cd django/`  
`ls`  
`virtualenv`  
`virtualenv --system-site packages -p python3 env/`  
`ls`  
`source env/bin/activate`  
`which pip`  
`ls`  
`micro requirements.txt` <--- tänne django  
`cat requirements.txt`  
`which pip`  
`pip install -r requirements.txt`  
`pip --version`    
`which pip3`    
`ls -l /home/nicklas/django/env/bin/pip3`  
`./manage.py runserver` (käynnistää)  
`django-admin startproject projektin nimi`  

---

##### HTML5 pohja

    <!DOCTYPE html>  
    <html lang="fi">    
      <head>  
        <title>otsikko</title>  
        <meta charset="utf-8" />  
        <style></style>    
      </head>  

      <body id="main">  
        <div>  
          <h1>Tervetuloa</h1>  
          <p>More coming soon...</p>  
        </div>  
      </body>  
    </html>  

---

#### Insert Guest Additions CD image..

`cd /media/nicklas/VBox_GAs_7.0.14/`  
`ls`  
`sudo bash VBoxLinuxAdditions.run`  

---

#### Tulimuuri

`sudo apt-get update`  
`sudo apt-get install ufw`  
`sudo ufw allow 80/tcp`  
`sudo ufw enable`  
  
---

#### ssh avaimen kopiointi

`ssh-copy-id tunnus@iposoite`  
