Viisikko
===
###### 25.10.2025.


###### 0:31

Järjestelmä:

Järjestelmän malli: Aspire E5-573G

Käyttöjärjestelmä: Microsoft Windows 10 Home

Suoritin: Inter(R) Pentium(R) 3558U @ 1.70GHz. Mhz, 2 ydin(tä)

Muisti: 6.00 Gt asennettua fyysistä muistia

USB-tikku: PNY 32 GB USB 3.1

-----
Aloitan syöttämällä tutut komennot, kuten: ```sudo apt-get update ``` ``` sudo apt-get -y dist-upgrade ``` ``` sudo apt-get -y install ufw ``` ```sudo ufw enable ```  
Lopuksi aikavyöhykkeen asentamista, jotta ohjelmat toimivat oikein: ```timedatectl ``` ```timedatectl list-timezones``` ``` sudo timedatectl set-timezone Europe/Helsinki ```
```timedatectl ```

x) Lue ja tiivistä
===
Karvinen 2025: Install Salt on Debian 13 Trixie:
- Salt on hallintatyökalu, joka mahdollistaa Windows - koneiden ja Linux - koneiden ohjaamisen yhtäaikaisesti.
- Salt ei ole Debianin vakio-ohjelmalähteissä, joten tarvitaan uusi apt-repositorio.
- Uusi apt-repositorio koostuu kahdesta tiedostosta:
- PGP-julkinen avain – ohjelmatiedostoihin luotetaan, kun niiden allekirjoitus vastaa tätä avainta.

Karvinen 2023: Run Salt Command Locally
- Salt-komentoja voi ajaa paikallisesti, jolloin näet tulokset heti – hyvä harjoitteluun ja testaukseen.
- Salt toimii sekä Linuxissa että Windowsissa, joten samoja komentoja voi käyttää molemmissa.
- Tärkeimmät Saltin tilatoiminnot ovat: ```pkg```, ```file```, ```service```, ```user``` ja ```cmd```.

Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux
- Saltilla voit hallita tuhansia tietokoneita yhdestä palvelimesta.
- Ohjattavat koneet (minionit) voivat olla missä tahansa – NATin tai palomuurin takana – kunhan master-palvelimella on julkinen IP-osoite.
- Opettele kirjoittamaan state-tiedostoja, jotka määrittelevät minionien tavoitetilan.

Karvinen 2006: Raportin kirjoittaminen
- Viittaa lähteisiin – se osoittaa perehtyneisyyttä ja noudattaa akateemista käytäntöä.
- Raportointi auttaa selkeyttämään ajatuksia ja säästämään aikaa, kun ei tarvitse toistaa kokeita.
- Hyvä raportti toimii myös ohjeistuksen pohjana muille.

###### 1:31
###### 6:44

Asenna Debian 13-Trixie virtuaalikoneeseen. (Poikkeuksellisesti tätä alakohtaa ei tarvitse raportoida, jos siinä ei ole mitään ongelmia. Mutta jos on ongelmia, sitten täsmällinen raportti, jotta voidaan ratkoa niitä yhdessä.) Asensin Debian 13 Live - tikulle, koska Virtuaalikone ei toiminut koneellani. 

b) Asenna Salt (salt-minion) Linuxille (uuteen virtuaalikoneeseesi).

Asennus ei alkuun onnistunut. Ratkaisuksi osottautui 
<img width="884" height="367" alt="Image" src="https://github.com/user-attachments/assets/5ce152fb-b2d6-496d-88f5-7ec1a78a2107" />

