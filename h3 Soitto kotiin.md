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



-----


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

###### 9.11.2025.
###### 22:40

a) Hello Vagrant! Osoita jollain komennolla, että Vagrant on asennettu (esim tulostaa vagrantin versionumeron). Jos et ole vielä asentanut niitä, raportoi myös Vagrant ja VirtualBox asennukset. (Jos Vagrant ja VirtualBox on jo asennettu, niiden asennusta ei tarvitse tehdä eikä raportoida uudelleen.):



<img width="513" height="197" alt="Sieppaa" src="https://github.com/user-attachments/assets/c3801d5f-f45b-4dab-b7de-f602becee266" />

###### 22:56 

b) Linux Vagrant. Tee Vagrantilla uusi Linux-virtuaalikone.

Suoritan Windowsin kautta seuraavat komennot:


    mkdir vagrant-kansio
    cd vagrant-kansio
    vagrant init debian/bookworm64
    vagrant up
    vagrant ssh
    whoami
    exit
    vagrant destroy


<img width="460" height="283" alt="Sieppaa1" src="https://github.com/user-attachments/assets/bf4bc3fd-fb63-4245-8326-22df3f0b2d37" />

Lopputulos.

###### 23:05

c) Kaksin kaunihimpi. Tee kahden Linux-tietokoneen verkko Vagrantilla. Osoita, että koneet voivat pingata toisiaan.


<img width="938" height="781" alt="Sieppaa5" src="https://github.com/user-attachments/assets/2b40bcb3-e094-464e-a953-379df6282af3" />



Lisäsin tämän VSCodeen. Osoitteesta: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/.

Tämän jälkeen luon uudelleen virtuaalikoneen, jotta niitä on kaksi kappaletta.



cd vagrant-kansio

vagrant init

config.vm.box = "debian/bookworm64" 

Vagrant up

Vagrant ssh t001

ping 192.168.88.102 

exit

Vagrant ssh t002

ping 192.168.88.101

exit

vagrant destroy

<img width="566" height="108" alt="Sieppaa3" src="https://github.com/user-attachments/assets/baa9fe78-9b6d-4865-baf2-bf0e4fe94151" />

###### 10.11.2025.
###### 0:07

En päässyt tästä eteenpäin. Katsoin polun, mutta en saanut pingattua näitä kahta konetta. 



-----
Lahteet
===

Fuentes, A, D 2021. How to install VirtualBox, Vagrant and a Virtual Machine in Windows 10. Katsottavissa: https://www.youtube.com/watch?v=krDU3BtJNpk. Katsottu: 9.11.2025.

Github 2025. Oppilas777/Linux-course. Luettavissa: https://github.com/Oppilas777/linux-course/blob/main/h7.md. Luettu: 4.11.2025.

Github 2025. Oppilas777/linux-course. Luettavissa: https://github.com/Oppilas777/linux-course. Luettu: 4.11.2025.

Github 2025. Oppilas777/linux-course. Luettavissa: https://github.com/Oppilas777/linux-course/blob/main/h6.md. Luettu: 4.11.2025.

Github 2025. Oppilas777/Palvelinten-hallinta. Luettavissa: https://github.com/Oppilas777/Palvelinten-hallinta/blob/main/h0%20Hei%20webbi.md. Luettu: 4.11.2025.

Github 2025. Oppilas777/Palvelinten-hallinta. Luettaviss: https://github.com/Oppilas777/Palvelinten-hallinta/blob/main/h2%20Infraa%20koodina.md. Luettu: 4.11.2025.

Github 2024. Thsoin. Luettavissa: https://github.com/thsoini/linux-course/blob/main/H2.md Luettu: 10.11.2025.

Hashicorp. Install Vagrant 2025. Luettavissa: https://developer.hashicorp.com/vagrant/docs/installation. Luettu: 9.11.2025.

Karvinen T. 2006. Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/. Luettu: 4.11.2025.

Karvinen T. 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux Luettavissa: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Luettu: 4.11.2025.

Karvinen T. 2025. Palvelinten Hallinta Configuration Management Systems course - 2025 spring Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 4.11.2025.

Karvinen T. 11.4.2021. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=Two%20Machine%20Virtual%20Network%20With%20Debian%2011%20Bullseye%20and%20Vagrant. Luettu: 4.11.2025.

Karvinen T. 28.3. 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. Luettu: 4.11.2025.

Karvinen T. 28.3. 2023. Salt Vagrant - automatically provision one master and two slaves. Luettavissa: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file. Luettu: 4.11.2025.

Linux (DEB) 2025. Salt Install Guide. Luettavissa: https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html. Luettu: 10.11.2025.
