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



