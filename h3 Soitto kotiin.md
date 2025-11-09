Soitto kotiin
===

###### 4.11.2025.
###### 10:54 

Järjestelmä:

Järjestelmän malli: Aspire E5-573G

Käyttöjärjestelmä: Microsoft Windows 10 Home

Suoritin: Inter(R) Pentium(R) 3558U @ 1.70GHz. Mhz, 2 ydin(tä)

Muisti: 6.00 Gt asennettua fyysistä muistia

Oracle Virtualbox

Debian 13 (trixie)


-----

Aloitan syöttämällä tutut komennot, kuten: ```sudo apt-get update ``` ```sudo dpkg --configure -a``` ``` sudo apt-get -y dist-upgrade ``` ``` sudo apt-get -y install ufw ``` ```sudo ufw enable ```  
Lopuksi aikavyöhykkeen asentamista, jotta ohjelmat toimivat oikein: ```timedatectl status``` ```timedatectl list-timezones``` ``` sudo timedatectl set-timezone Europe/Helsinki``` ```sudo timedatectl set-ntp true```



----


###### 11:05 


x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva. Ei siis vaadita pitkää eikä essee-muotoista tiivistelmää.)

Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant (Huomaa: nykyinen Debian stable on 12-Bookworm, Vagrantissa "debian/bookworm64". Vanhentunutta 11-bullseye:ta ei enää käytetä):

- Vagrant mahdollistaa sen, että sillä voi harjoitella verkottamista ja automaatiota.
- SSH-yhteydes voidaan suorittaa yhdellä komennolla.
- Tuhoa koneet: ```vagrant destroy``` Luo: uudelleen: ```vagrant up```


Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux (Huomaa: Nykyisin ennen Saltin asentamista on asennettava ensin varasto [package repository], ohje h1 vinkeissä):

- Mahdollistaa sen, etta voit hallita tuhansia koneita yhdestä master-palvelimesta.
- Vain masterin tarvitsee olla julkisesti saavutettavissa, ja minionit voivat olla minka tahansa verkon, kuten NATin, palomuurin tai tuntemattoman domainin - takana.
- Masterin asennus, komennolla: ```sudo apt-get -y install salt-master``` Tarkista IP-osoite: ```hostname -I```
- Avaimen hyvaksyntä: ```sudo salt-key -A```


Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves, vain kohdat:

Infra as Code - Your wishes as a text file:

- Mahdollistaa halutun tilan tekstinä YAML-muodossa.
- Kaytä Saltin state-tiedostoja automatisoimaan konfiguraatioita.
- Luo kansio komennolla: ```sudo mkdir -p /srv/salt/hello``` ja sen jälkeen luo tiedosto: ```udoedit /srv/salt/hello/init.sls```
- Sisällön luomisessa, muita kaksi valilyontia ja aseta:  ```/tmp/infra-as-code:
  file.managed ```
- Lopuksi aja masterilla: Käynnistä tila kaikille minioneille: ```sudo salt '*' state.apply hello```
- Lopputulos: Tämä luo tiedoston ```/tmp/infra-as-code kaikille minioneille```



top.sls - What Slave Runs What States:

- Top.sls määrittää, mitkä tilat (states) ajetaan mille minioneille.
- Käytetään, jotta ei tarvitse erikseen nimetä state-moduuleja komentorivillä.
- Määrita: ```sudo salt '*' state.apply```
- Yaml sisalto esimerkkinä: ```base: '*':- hello``` Muista välilyonni kirjoittaessasi näitä!


###### 11:49
Tauko
###### 

a) Hello Vagrant! Osoita jollain komennolla, että Vagrant on asennettu (esim tulostaa vagrantin versionumeron). Jos et ole vielä asentanut niitä, raportoi myös Vagrant ja VirtualBox asennukset. (Jos Vagrant ja VirtualBox on jo asennettu, niiden asennusta ei tarvitse tehdä eikä raportoida uudelleen.):



<img width="513" height="197" alt="Sieppaa" src="https://github.com/user-attachments/assets/c3801d5f-f45b-4dab-b7de-f602becee266" />

###### 14:00 
###### 8.11.2025.
###### 4:48


###### 22:50

b) Linux Vagrant. Tee Vagrantilla uusi Linux-virtuaalikone.






-----
Lahteet
===

Fuentes, A, D 2021. How to install VirtualBox, Vagrant and a Virtual Machine in Windows 10. Katsottavissa: https://www.youtube.com/watch?v=krDU3BtJNpk. Katsottu: 9.11.2025.

Github 2025. Oppilas777/Linux-course. Luettavissa: https://github.com/Oppilas777/linux-course/blob/main/h7.md. Luettu: 4.11.2025.

Github 2025. Oppilas777/linux-course. Luettavissa: https://github.com/Oppilas777/linux-course. Luettu: 4.11.2025.

Github 2025. Oppilas777/linux-course. Luettavissa: https://github.com/Oppilas777/linux-course/blob/main/h6.md. Luettu: 4.11.2025.

Github 2025. Oppilas777/Palvelinten-hallinta. Luettavissa: https://github.com/Oppilas777/Palvelinten-hallinta/blob/main/h0%20Hei%20webbi.md. Luettu: 4.11.2025.

Github 2025. Oppilas777/Palvelinten-hallinta. Luettaviss: https://github.com/Oppilas777/Palvelinten-hallinta/blob/main/h2%20Infraa%20koodina.md. Luettu: 4.11.2025.

Hashicorp. Install Vagrant 2025. Luettavissa: https://developer.hashicorp.com/vagrant/docs/installation. Luettu: 9.11.2025.

Karvinen T. 2006. Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/. Luettu: 4.11.2025.

Karvinen T. 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux Luettavissa: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Luettu: 4.11.2025.

Karvinen T. 2025. Palvelinten Hallinta Configuration Management Systems course - 2025 spring Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 4.11.2025.

Karvinen T. 11.4.2021. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=Two%20Machine%20Virtual%20Network%20With%20Debian%2011%20Bullseye%20and%20Vagrant. Luettu: 4.11.2025.

Karvinen T. 28.3. 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. Luettu: 4.11.2025.

Karvinen T. 28.3. 2023. Salt Vagrant - automatically provision one master and two slaves. Luettavissa: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file. Luettu: 4.11.2025.

