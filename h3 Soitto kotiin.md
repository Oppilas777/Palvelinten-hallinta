Soitto kotiin
===

###### 4.11.2025.
###### 10:54 

Järjestelmä:

Järjestelmän malli: Aspire E5-573G

Käyttöjärjestelmä: Microsoft Windows 10 Home

Suoritin: Inter(R) Pentium(R) 3558U @ 1.70GHz. Mhz, 2 ydin(tä)

Muisti: 6.00 Gt asennettua fyysistä muistia

USB-tikku: PNY 32 GB USB 3.1

Debian 13 (trixie)


-----

Aloitan syöttämällä tutut komennot, kuten: ```sudo apt-get update ``` ``` sudo apt-get -y dist-upgrade ``` ``` sudo apt-get -y install ufw ``` ```sudo ufw enable ```  
Lopuksi aikavyöhykkeen asentamista, jotta ohjelmat toimivat oikein: ```timedatectl status``` ```timedatectl list-timezones``` ``` sudo timedatectl set-time 2025-10-28 10:30:00 ```
```timedatectl ```

-----

###### 11:05 


x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva. Ei siis vaadita pitkää eikä essee-muotoista tiivistelmää.)

Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant (Huomaa: nykyinen Debian stable on 12-Bookworm, Vagrantissa "debian/bookworm64". Vanhentunutta 11-bullseye:ta ei enää käytetä):

- Vagrant ahdollistaa harjoitella verkottamista ja automaatiota.
- SSH-yhteydes voidaan suorittaa yhdellä komennolla.
- Tuhoa koneet: ```vagrant destroy``` Luo: uudelleen: ```vagrant up```


Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux (Huomaa: Nykyisin ennen Saltin asentamista on asennettava ensin varasto [package repository], ohje h1 vinkeissä):

- Mahdollistaa sen, etta voit hallita tuhansia koneita yhdestä master-palvelimesta.
- Vain masterin tarvitsee olla julkisesti saavutettavissa, ja minionit voivat olla minka tahansa verkon, kuten NATin, palomuurin tai tuntemattoman domainin - takana.
- Masterin asennus, komennolla: ```sudo apt-get -y install salt-master``` Tarkista IP-osoite: ```hostname -I```
- Avaimen hyvaksynta: ```sudo salt-key -A```


Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves, vain kohdat:

Infra as Code - Your wishes as a text file:

- Mahdollistaa halutun tilan tekstinä YAML-muodossa.
- Kayta Saltin state-tiedostoja automatisoimaan konfiguraatioita.
- Luo kansio komennolla: ```sudo mkdir -p /srv/salt/hello``` ja sen jalkeen luo tiedosto: ```udoedit /srv/salt/hello/init.sls```
- Sisallon luomisessa, muita kaksi valilyontia ja aseta:  ```/tmp/infra-as-code:
  file.managed ```
- Lopuksi aja masterilla: Käynnistä tila kaikille minioneille: ```sudo salt '*' state.apply hello```
- Lopputlous: Tämä luo tiedoston ```/tmp/infra-as-code kaikille minioneille```



top.sls - What Slave Runs What States:

- Top.sls määrittää, mitkä tilat (states) ajetaan mille minioneille.
- Käytetään, jotta ei tarvitse erikseen nimetä state-moduuleja komentorivillä.
- Maarita: ```sudo salt '*' state.apply```
- Yaml sisalto esimerkkina: ```base: '*':- hello``` Muista valilyonnit naissa!


###### 11:49
Tauko
###### 

a) Hello Vagrant! Osoita jollain komennolla, että Vagrant on asennettu (esim tulostaa vagrantin versionumeron). Jos et ole vielä asentanut niitä, raportoi myös Vagrant ja VirtualBox asennukset. (Jos Vagrant ja VirtualBox on jo asennettu, niiden asennusta ei tarvitse tehdä eikä raportoida uudelleen.):

Live-tikulla ei ollut saatavilla valmiina, joten aloitin komennolla: ```sudo apt install vagrant``` Minka jalkeen: ```vagrant --version```

VirtualBox ei ollut saatavilla, joten latasin Libvirtin, komennolla:  ```sudo apt update ```

 ```sudo apt install libvirt-daemon-system libvirt-clients qemu-kvm vagrant-libvirt ```

 Palvelun kayttoon ottaminen ja kaynnistaminen tapahtui seuraavanlaisesti: ```sudo systemctl enable --now libvirtd```

 Asentaminen oli aikaa vieva prosessi, koska tiekoneesta loppui tila, ja jouduin tekemaan kaiken alusta loppuun, uudelleen

 
<img width="741" height="481" alt="Image" src="https://github.com/user-attachments/assets/71fbfa04-c0f3-4a82-b3a0-f40cd9425194" />

Versinumero ja libvrt asennettu!


###### 14:00 
###### 8.11.2025.
###### 4:48


b) Linux Vagrant. Tee Vagrantilla uusi Linux-virtuaalikone.

Tehtavien tyostaminen jatkuu. Perustoiminnot suoritettu, kuten sudo apt-get update suoritettu.

Live-tikulla asentaminen ei onnistunut tavalliseen tapaan, joten paadyin vaihtoehtoiseen tapaan suorittaa tehtava b. Tama siita syysta, että VirtualBoxin asennus ei onnistunut taysin — komentoa vboxmanage ei löytynyt, eikä vboxconfig ollut saatavilla. Tämä viittaa ehka siihen, että VirtualBoxin ydinkomponentit eivät ole saatavilla, tai ne eivät ole yhteensopivia live-USB-ympäristön kanssa.

Kysyin CoPilotilta apua tassa vaiheessa, joka neuvoi seuraavanlaiset komennot:

KVM ja Libvirtin asennus: 

```sudo apt update```

```sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager```

Vagrantin libvirt-tuki asennus:

```sudo apt install vagrant vagrant-libvirt```

<img width="738" height="522" alt="Image" src="https://github.com/user-attachments/assets/3001c8ae-e030-49a7-86ce-60f78630693b" />

Virtuaalikoneen kaynnistaminen librvirtin kautta.



<img width="739" height="507" alt="Image" src="https://github.com/user-attachments/assets/78da5c19-02be-4e9a-bf84-4c6bc5c8d576" />

Taman jalkeen: ```sudo systemctl restart libvirtd``` oppitunnin ohjeiden mukaisesti. 

Kuvan perusteella voidaan olettaa, etta libvirtin palvelu (libvirtd) on nyt aktiivinen ja käynnissä oikein:

    ✅ Active: active (running)

    ✅ dnsmasq-prosessit pyörivät — tämä hoitaa DHCP:n

    ✅ Ei virheilmoituksia




Luodaan uusi hakemisto projektille: ```mkdir vagrant-linux-vm``` ```cd vagrant-linux-vm``` 

Taman jalkeen projektin alustaminen: ```vagrant init generic/debian12```

```curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg```

```echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \```
```https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \```
```sudo tee /etc/apt/sources.list.d/hashicorp.list```

```sudo apt update```
```sudo apt install vagrant -y```










-----
Lahteet
===

Github 2025. Oppilas777/Linux-course. Luettavissa: https://github.com/Oppilas777/linux-course/blob/main/h7.md. Luettu: 4.11.2025.

Github 2025. Oppilas777/linux-course. Luettavissa: https://github.com/Oppilas777/linux-course. Luettu: 4.11.2025.

Github 2025. Oppilas777/linux-course. Luettavissa: https://github.com/Oppilas777/linux-course/blob/main/h6.md. Luettu: 4.11.2025.

Github 2025. Oppilas777/Palvelinten-hallinta. Luettavissa: https://github.com/Oppilas777/Palvelinten-hallinta/blob/main/h0%20Hei%20webbi.md. Luettu: 4.11.2025.

Github 2025. Oppilas777/Palvelinten-hallinta. Luettaviss: https://github.com/Oppilas777/Palvelinten-hallinta/blob/main/h2%20Infraa%20koodina.md. Luettu: 4.11.2025.

Karvinen T. 2006. Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/. Luettu: 4.11.2025.

Karvinen T. 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux Luettavissa: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Luettu: 4.11.2025.

Karvinen T. 2025. Palvelinten Hallinta Configuration Management Systems course - 2025 spring Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 4.11.2025.

Karvinen T. 11.4.2021. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. Luettu: 4.11.2025.

Karvinen T. 28.3. 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. Luettu: 4.11.2025.

Karvinen T. 28.3. 2023. Salt Vagrant - automatically provision one master and two slaves. Luettavissa: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file. Luettu: 4.11.2025.

