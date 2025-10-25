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
Tässä välissä käynnistin koneen surffailin netissä, ja tutustuin uuteen päivitykseen. Linuxin ladattuani tutustuin myös uuteen käyttöjärjestelmään. 
###### 6:44

Asenna Debian 13-Trixie virtuaalikoneeseen. (Poikkeuksellisesti tätä alakohtaa ei tarvitse raportoida, jos siinä ei ole mitään ongelmia. Mutta jos on ongelmia, sitten täsmällinen raportti, jotta voidaan ratkoa niitä yhdessä.) Asensin Debian 13 Live - tikulle, koska Virtuaalikone ei toiminut koneellani. 

b) Asenna Salt (salt-minion) Linuxille (uuteen virtuaalikoneeseesi).

Asennus onnistui, mutta tarvittavia testeja ei voitu alussa suorittaa. Ongelma korjaantui lopulta.
<img width="884" height="367" alt="Image" src="https://github.com/user-attachments/assets/5ce152fb-b2d6-496d-88f5-7ec1a78a2107" />

c) Viisi tärkeintä. Näytä Linuxissa esimerkit viidestä tärkeimmästä Saltin tilafunktiosta: pkg, file, service, user, cmd. Analysoi ja selitä tulokset.

Pkg.installed - Asenna paketti! Ajettiin Komento ```sudo ~/salt-venv/bin/salt-call --local state.single pkg.installed name=vim```

Salt ei asentanut pakettia uudelleen, eikä muuttanut järjestelmää. Ohjelmapalautti onnistuneen tuloksen ilman muutoksia

<img width="884" height="367" alt="Image" src="https://github.com/user-attachments/assets/a0fa66ef-57b1-41ea-8982-6b6f777aaa67" />


file.managed – Luo tiedosto! Komento ```sudo ~/salt-venv/bin/salt-call --local state.single file.managed name=/tmp/salt-test.txt contents="Hei Salt!" user=root group=root mode=644```

<img width="737" height="403" alt="Image" src="https://github.com/user-attachments/assets/d441aed8-c629-47c5-b28e-c9294c7e5ed6" />

Tiedosto on olemassa. Sen sisältö on "Hei Salt!" Omistajuus ja käyttöoikeudet ovat oikein.

Sservice.running – Käynnistä palvelu! Ajettiin komento ```sudo ~/salt-venv/bin/salt-call --local state.single service.running name=ssh enable=True```

<img width="738" height="406" alt="Image" src="https://github.com/user-attachments/assets/662cff70-34d8-4ac5-be2f-1a573c1f9f2f" />

Tämä tuloste kertoo, että Saltin service.running-tilafunktio epäonnistui, koska se ei löytänyt palvelua nimeltä ssh. Salt yrittää hallita palvelua nimeltä ssh, mutta Debian-järjestelmässä palvelun nimi voi olla: ssh (jos käytetään OpenSSH:n palvelunimeä) tai sshd (yleisempi nimi OpenSSH-palvelulle)


User.account - Luo käyttäjä! Komento ```sudo ~/salt-venv/bin/salt-call --local state.single user.present name=testuser shell=/bin/bash home=/home/testuser```

<img width="610" height="945" alt="Image" src="https://github.com/user-attachments/assets/274faad7-8586-4e40-84fd-95c1dd8ae869" />

Tämä oli ensimmäinen ajokerta, joten Salt: Loi käyttäjän testuser. Asetti kotihakemiston ja shellin sekä ryhmän.

Raportoi muutokset Changes-kentässä. Toistettavuus: Voit ajaa tilan uudelleen ilman pelkoa tuplakäyttäjistä tai virheistä.

cmd.run! Komento ```sudo ~/salt-venv/bin/salt-call --local state.single cmd.run name='echo "Salt toimii!" > /tmp/salt-output.txt' creates=/tmp/salt-output.txt```

<img width="918" height="629" alt="Image" src="https://github.com/user-attachments/assets/afafffba-1a02-4412-8d3e-74c2b6bbd2b5" />

Salt tarkisti järjestelmän tilan ja havaitsi, että vim-paketti on jo asennettu. Koska tila oli jo halutussa muodossa: ei asentanut pakettia uudelleen, eikämuuttanut järjestelmää.
Ohjelma palautti onnistuneen tuloksen ilman muutoksia. Tämä on idempotenssin ydin: tila voidaan ajaa monta kertaa, mutta järjestelmä ei muutu enää, kun se on kunnossa.


d) Idempotentti. Anna esimerkki idempotenssista. Aja 'salt-call --local' komentoja, analysoi tulokset, selitä miten idempotenssi ilmenee.

Komento  ```sudo ~/salt-venv/bin/salt-call --local state.single file.symlink name=/tmp/linkki.txt target=/tmp/salt-test.txt```

<img width="739" height="479" alt="Image" src="https://github.com/user-attachments/assets/227a62e4-e049-4b3f-9a56-c66d6f5d56d9" />

Symboliset linkit voivat helposti mennä rikki tai osoittaa väärään paikkaan. Tämä varmistaa, että linkki on olemassa ja osoittaa oikeaan kohteeseen. Jos kaikki on kunnossa, Salt ei tee muutoksia.

Group.present - ryhmän luonti Komento ```sudo ~/salt-venv/bin/salt-call --local state.single group.present name=saltgroup```

Tämä oli ensimmäinen ajokerta, joten Salt: Loi ryhmän saltgroup Asetti sille GID:n ja muut oletusominaisuudet Raportoi muutokset Changes-kentässä.

<img width="508" height="470" alt="Image" src="https://github.com/user-attachments/assets/d47f0e3c-2413-4d96-a900-011472df8805" />


###### 9:02

-----
Lähdeviitteet

https://github.com/jerebjo/Palvelinten-hallinta/blob/main/H1%20viisikko.md

https://terokarvinen.com/palvelinten-hallinta/#laksyt

https://terokarvinen.com/install-salt-on-debian-13-trixie/

https://terokarvinen.com/2021/salt-run-command-locally/

https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/

https://github.com/Oppilas777/linux-course/blob/main/h6.md

https://github.com/Oppilas777/linux-course

https://terokarvinen.com/2021/install-debian-on-virtualbox/

