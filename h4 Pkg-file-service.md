Pkg-file-service
===

###### 12.11.2025.
###### 8:26 

Järjestelmä:

Järjestelmän malli: Aspire E5-573G

Käyttöjärjestelmä: Microsoft Windows 10 Home

Suoritin: Inter(R) Pentium(R) 3558U @ 1.70GHz. Mhz, 2 ydin(tä)

Muisti: 6.00 Gt asennettua fyysistä muistia

Oracle Virtualbox

Debian 13 (trixie)

-----


Aloitan syöttämällä tutut komennot, kuten: 

```
sudo apt-get update
sudo dpkg --configure -a
sudo apt-get -y dist-upgrade
sudo apt-get -y install ufw \
sudo ufw enable 
```

Lopuksi aikavyöhykkeen asennus, jotta ohjelmat toimivat oikein: 

```
sudo timedatectl set-timezone Europe/Helsinki
sudo timedatectl
set-ntp true
```
-----

###### 8:37

x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)

Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port

Artikkelissa on esimerkkinä jonkun toisen Linux-version sshd_config tiedosto. Jos tekisit samanlaisen, niin käyttäisit tietysti oman järjestelmäsi asetustiedostoa pohjana.

- Konfiguraationhallintajärjestelmällä voidaan hallita suurta määrää daemoneja.
  Yleinen toimintamalli on package-file-service: ensin asennetaan tarvittava ohjelmisto sen jälkeen korvataan konfiguraatiotiedosto
  lopuksi käynnistetään daemon uudelleen, jotta uusi konfiguraatio otetaan käyttöön.

- Artikkelissa esitellään yksinkertainen Salt-tila, jolla vaihdetaan SSH-palvelimen portti. Ensin määritetään Saltin master–slave-      arkkitehtuuri. Master-palvelimelle luodaan tila nimeltä sshd.sls.Masterille tallennetaan myös konfiguraatiotiedoston pääkopio         (sshd_config).


Luodaan SSH_tila:
```
cat /srv/salt/sshd.sls
openssh-server:
 pkg.installed
/etc/ssh/sshd_config:
 file.managed:
   - source: salt://sshd_config
sshd:
 service.running:
   - watch:
     - file: /etc/ssh/sshd_config
```

Salt - tilan kaytoon ottaminen tapahtuu seuraavanalisesti:
```
sudo salt '*' state.apply sshd
```

Testaaminen:
```
nc -vz tero.example.com 8888
Connection to tero.example.com 2002 port [tcp/*] succeeded!
```
Vaihtoehtoinen tapa:
```
ssh -p 8888 tero@tero.example.com
tero@tero.example.com's password:
```

Ja muistutuksena, moduli omaan kansioonsa, eli /srv/salt/ssh/init.sls (eikä hujan hajan /srv/salt/ssh.sls)

###### 9:25
-----

###### 9:35

a) SSHouto. Lisää uusi portti, jossa SSHd kuuntelee.

Aloitan lataamalla Vagrant debianille. Tata ennen olin ladannut sen Windowsille. 

Lisäätään HashiCorpin APT-avaimet ja repositorio. Näin varmisttaan samalla, että versio on uusin.

```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```


Seuraavaksi pakettiliastan päivitys ja Vagrantin - asennus.
```
sudo apt update
sudo apt install vagrant
```
Kolmas vaihde, jossa varmistetaan, etta asennus on valmiina:




Lähteet 
-----

GitHub 2025. Joonas Janttonen. Laksyt. Luettavissa: https://github.com/JoonasJanttonen/Palvelinten-hallinta/edit/main/h3%20Soitto%20kotiin.md. Luettu: 12.11.2025.

Tero Karvinen 2025. Palvelinten hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 12.11.2025.

Tero Karvinen 2018. Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh. Luettu: 12.11.2025.

Tero Karvinen 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Luettu: 12.11.2025.
