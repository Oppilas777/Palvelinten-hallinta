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
```sudo apt-get update ``` ```sudo dpkg --configure -a``` ``` sudo apt-get -y dist-upgrade ``` ``` sudo apt-get -y install ufw ``` ```sudo ufw enable ```

Lopuksi aikavyöhykkeen asennus, jotta ohjelmat toimivat oikein: ```timedatectl status``` ```timedatectl list-timezones``` ``` sudo timedatectl set-timezone Europe/Helsinki``` ```sudo timedatectl set-ntp true```



{sudo apt-get update}

-----


###### 8:37

x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)

Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port

Artikkelissa on esimerkkinä jonkun toisen Linux-version sshd_config tiedosto. Jos tekisit samanlaisen, niin käyttäisit tietysti oman järjestelmäsi asetustiedostoa pohjana.

- 

















Lahteet
-----

GitHub 2025. Joonas Janttonen. Laksyt. Luettavissa: https://github.com/JoonasJanttonen/Palvelinten-hallinta/edit/main/h3%20Soitto%20kotiin.md. Luettu: 12.11.2025.

Tero Karvinen 2025. Palvelinten hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 12.11.2025.

Tero Karvinen 2018. Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh. Luettu: 12.11.2025.

Tero Karvinen 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Luettu: 12.11.2025.
