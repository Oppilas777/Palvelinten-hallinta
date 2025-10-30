Infraa koodina
===
###### 29.10.2025
###### 20:51

Järjestelmä:

Järjestelmän malli: Aspire E5-573G

Käyttöjärjestelmä: Microsoft Windows 10 Home

Suoritin: Inter(R) Pentium(R) 3558U @ 1.70GHz. Mhz, 2 ydin(tä)

Muisti: 6.00 Gt asennettua fyysistä muistia

USB-tikku: PNY 32 GB USB 3.1

-----

Aloitan syöttämällä tutut komennot, kuten: ```sudo apt-get update ``` ``` sudo apt-get -y dist-upgrade ``` ``` sudo apt-get -y install ufw ``` ```sudo ufw enable ```  
Lopuksi aikavyöhykkeen asentamista, jotta ohjelmat toimivat oikein: ```timedatectl status``` ```timedatectl list-timezones``` ``` susudo timedatectl set-time 2025-10-28 10:30:00 ```
```timedatectl ```

------

###### 21:06

x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)

Karvinen 2014: Hello Salt Infra-as-Code:

- Salt mahdollistaa tuhansien kondeiden hallitsemisen. 
- Salt on konfiguraationhallintajarjestelma.
- Idempotenssi tarkoittaa sita, etta toimenpiteen uusiminen/toistaminen ei muokkaa lopputulosta. mikali se on jo saavutettu. Tama on tarkeaa Saltin kaytossa.
    

Salt contributors: Salt overview, kohdat:

Rules of YAML:

- Tieto esitetaan avain: arvo-pareina. Arvot voivat olla eri muodoissa. 
- Avain ja arvo erotetaan kaksoispisteellä ja yhdellä välilyönnillä.  Esimerkiksi: ```nimi: Joonas```
- Oikein: ikä: 30 / Väärin: ```ikä:30``` tai ```ikä : 30```
- Aloita risuaitamerkillä #  Esimerkiksi: ```# Suorita uudelleen```

YAML simple structure:

- YAML sisaltaa kolme peruselementtia. Scalareita, eli yksittaisia arvoja, kuten merkkijona ja numero. Listat, eli avaimet, joita seuraa arvo ```- ```merkilla. Seka sanakirjat. Eli sanakirjat sisaltavat sanakirjoja, mitka sisaltavat arvoja.
- YAML perustuu lohkorakenteeseen, ja sisennys maarittaa kontekstin.
- Kaksi valilyontia on standardi, kun kaytetaan sisennysta.

Lists and dictionaries - YAML block structures:

- Kaksi valilyontia riittaa.
- Kokoelmat, kuten sanakirja tai listat ilmaistaan yhdysmerkillä ja välilyönnillä: - arvo. Esimerkki: ```- Appelsiini```
- Ala kayta sarkaimia, kuten oppitunnilla neuvottiin!

###### 21:43 
Tauko
###### 22:17

Salt contributors: Salt overview, kohdat:

Introduction:

- Jarjestelmanvalvojan maarittaa roolit koneiden ryhmille, jotta hallinta olisi helpompaa.
- ```top.sls``` sijaitsee aina hakemistopuun ylimmassa osassa.
- Yhdessa koneet muodostavat sovellupinot. Eng. Application stacks, joka tarkoittaa jarstelmaa mika on ik''n kuin kerroksittain rakennettu jarjestelma, jossa jokaisella on oma tehtava.


A basic example:

- Ymparisto on se, joka sisaltaa tilatiedot konfigurointiin.
- Koneista muodostettu ryhma, on kohde, johon tietty joukko tiloja sovelletaan.
- State Files on luettelo tiedostoista. Nama maarittaat ja valvovat konfiguraatiota.

###### 22:59  

###### 30.10.2025.

###### 6:38

Jatkan tehtavien tyostamista. Tahan mennessa olen suorittanut kaikki peruskomennot, kuten ```sudo apt-get update```


a) Hei infrakoodi! Kokeile paikallisesti (esim 'sudo salt-call --local') infraa koodina. Kirjota sls-tiedosto, joka tekee esimerkkitiedoston /tmp/ -kansioon.

Debian Trixie ei sisalla Saltia oletuksena, joten Copilotin avustuksella lisaan pakettivaraston, ennen projektia. Suoritan komennon: ```# Luo keyrings-hakemisto
sudo mkdir -p /etc/apt/keyrings``` 

Lataan Saltin julkinen avain
```curl -fsSL https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public | sudo tee /etc/apt/keyrings/salt-archive-keyring.pgp```

Seuraavaksi: ```curl -fsSL https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources | sudo tee /etc/apt/sources.list.d/salt.sources``` 

Taman jalkeen paivitys ja Saltin asennusta: ```sudo apt install salt-minion``` ```salt-call --version ``` 

Testaaminen onnistui, eli Salt toimii. 

Luodaan tarkistuslista: ```sudo mkdir -p /srv/salt/hellojoonas
sudo nano /srv/salt/hellojoonas/init.sls```

Lisaan Nanoon tiedot seuraavanlaisesti: ```create_example_file:
  file.managed:
    - name: /tmp/joonas.txt
    - contents: |
        Moi Joonas! Tämä tiedosto luotiin Saltilla.
    - mode: '644'
    - user: root
    - group: root```


b) Toppping. Tee top-file, niin että kaikki omat tilasi ajetaan kerralla komennolla 'sudo salt-call --local state.apply'.

c) Viisikko tiedostossa. Tee erilliset esimerkit kustakin viidestä tärkeimmästä tilafunktiosta pkg, file, service, user, cmd. Kirjoita esimerkit omiksi tiloikseen /srv/salt/ alle, esim /srv/salt/hellopkg/init.sls.

d) Tee sls-tiedosto, joka käyttää vähintään kahta eri tilafunktiota näistä: package, file, service, user. Tarkista eri ohjelmalla, että lopputulos on oikea. Osoita useammalla ajolla, että sls-tiedostosi on idempotentti.

sudo apt update
sudo apt install salt-minion
sudo mkdir -p /srv/salt/Uusi_kansio
cd /srv/salt/
sudo mkdir esimerkki
ls



------
Lahteet
===
Github 2025. jerebjo/palvelinten-hallinta. Luettavissa: https://github.com/jerebjo/Palvelinten-hallinta/blob/main/h3%20infraa%20koodina.md. Luettu: 29.10.2025.

Github 2025. Oppilas777/Linux-course. Luettavissa: https://github.com/Oppilas777/linux-course/blob/main/h7.md. Luettu: 29.10.2025.

Github 2025. Oppilas777/linux-course. Luettavissa: https://github.com/Oppilas777/linux-course. Luettu: 29.10.2025.

Github 2025. Oppilas777/linux-course. Luettavissa: https://github.com/Oppilas777/linux-course/blob/main/h6.md. Luettu: 29.10.2025.

Karvinen T. 2022. Comman line Basics revisted Luettavissa: https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=basic%20command. Luettu: 29.10.2025

Karvinen T. 2024. Hello Salt Infra-as-Code. Luettavissa: https://terokarvinen.com/2024/hello-salt-infra-as-code/. Luettu: 29.10.2025.

Karvinen T. 2006. Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/. Luettu: 29.10.2025.

Karvinen T. 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux Luettavissa: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Luettu: 29.10.2025.

Karvinen T. 2025. Run Salt Command Locally. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/. Luettu: 29.10.2025.

Karvinen T. 2025. Install Salt on Debian 13 Trixie. Luettavissa: https://terokarvinen.com/install-salt-on-debian-13-trixie/. Luettu: 29.10.2025.

Karvinen T. 2025. Palvelinten Hallinta Configuration Management Systems course - 2025 spring Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 29.10.2025.

Salt-Project 2025. Salt Overview. Luettavissa: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml. Luettu: 29.10.2025.

Salt-Project 2025. The Top File. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/top.html. Luettu: 29.10.2025.
