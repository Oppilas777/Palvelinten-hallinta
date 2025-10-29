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
Lähdeviitteet

Debian 2025.Debian 13 "trixie" released. Luettavissa: https://www.debian.org/News/2025/20250809. Luettu: 25.10.2025.

Github 2025. jerebjo/palvelinten-hallinta. Luettavissa: https://github.com/jerebjo/Palvelinten-hallinta/blob/main/H1%20viisikko.md. Luettu: 25.10.2025.

Github 2025. Oppilas777/linux-course. Luettavissa: https://github.com/Oppilas777/linux-course. Luettu: 25.10.2025.

Github 2025. Oppilas777/linux-course. Luettavissa: https://github.com/Oppilas777/linux-course/blob/main/h6.md. Luettu: 25.10.2025.

Karvinen T. 2006. Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/. Luettu: 25.10.2025.

Karvinen T. 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu LinuxLuettavissa: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Luettu: 25.10.2025.

Karvinen T. 2024. Install Debian on Virtualbox - Updated 2024. Luettavissa: https://terokarvinen.com/2021/install-debian-on-virtualbox/. Luettu: 25.10.2025.

Karvinen T. 2025. Run Salt Command Locally. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/. Luettu: 25.10.2025.

Karvinen T. 2025. Install Salt on Debian 13 Trixie. Luettavissa: https://terokarvinen.com/install-salt-on-debian-13-trixie/. Luettu: 25.10.2025.

Karvinen T. 2025. Palvelinten Hallinta Configuration Management Systems course - 2025 spring Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 25.10.2025.






sudo apt update
sudo apt install salt-minion
sudo mkdir -p /srv/salt/Uusi_kansio
cd /srv/salt/
sudo mkdir esimerkki
ls



https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=basic%20command
