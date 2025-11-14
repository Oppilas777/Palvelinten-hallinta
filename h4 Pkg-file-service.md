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

Salt - tilan käyttöön ottaminen:
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
Raportin muokkaamista.
###### 11:57
###### 13.11.2025.
###### 15:27 

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

<img width="741" height="63" alt="Image" src="https://github.com/user-attachments/assets/db2a4cfb-f372-45ff-925c-4f72bd4b02d9" />

<img width="537" height="290" alt="Screenshot From 2025-11-13 15-55-58" src="https://github.com/user-attachments/assets/d4da2768-7f99-4d67-8725-61a9a1fa0c5b" />

Varmistan, etta portti 22 on auki.

<img width="821" height="242" alt="Screenshot From 2025-11-13 17-29-52" src="https://github.com/user-attachments/assets/814659df-9153-476c-b6bb-6f7f6cb20d10" />

Tilanne.

<img width="829" height="403" alt="Screenshot From 2025-11-13 17-40-12" src="https://github.com/user-attachments/assets/0f1ecad5-04e2-4262-8d04-aaad8e37fb31" />

SSHd kuuntelee

###### 17:48 
###### 17:50 
b) Vapaaehtoinen, haastavahko tässä vaiheessa: Asenna ja konfiguroi Apache ja Name Based Virtual Host. Sen tulee näyttää palvelimen etusivulla weppisivua. Weppisivun tulee olla muokattavissa käyttäjän oikeuksin, ilman sudoa.

Syötin terminaalissa seuraavat käskyt:

```
sudo systemctl enable apache2
sudo nano /etc/apache2/sites-available/test.com.conf
sudo a2ensite example.com.conf
systemctl reload apache2
```
```
sudo nano /etc/hosts
sudo mkdir -p /var/www/example.com/public_html
sudo chown -R joonas:joonas /var/www/example.com
```
Seuraavaksi muokkasin sivuja.
```
echo '<html><body><h1>Welcome to example.com!</h1></body></html>' > /var/www/example.com/public_html/index.html
echo '<html><body><h1>Welcome to test.com!</h1></body></html>' > /var/www/test.com/public_html/index.html
```
Tarkistan, etta tiedostot ovat olemassa.
```
ls /var/www/example.com/public_html
ls /var/www/test.com/public_html
```
Varmistan, että sivu(t) käynnistyvät.
```
sudo nano /etc/hosts
sudo a2ensite example.com.conf
sudo systemctl reload apache2
sudo tail -f /var/log/apache2/error.log
```

<img width="975" height="646" alt="Screenshot From 2025-11-13 19-42-41" src="https://github.com/user-attachments/assets/5bbf150f-18c9-4065-aa2f-f951a024f048" />

Näkymä terminaalista. Tämän pitäisi vastaaa tehtävänantoa. 

<img width="977" height="157" alt="Screenshot From 2025-11-13 19-54-52" src="https://github.com/user-attachments/assets/d6300dd9-91aa-4ca9-af57-a5f923b4d9f6" />

Testisivu. Muokkasin terminaalin kautta.

###### 20:05


###### 14.11.2025.
###### 9:53 

c) Vapaaehtoinen, haastava: Caddy. Asenna Caddy tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.

Apache kaytti porttia 80. Poistin taman, jotta Caddy voisi kayttaa sita.

```
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
udo apt update
sudo apt install caddy
```

<img width="721" height="71" alt="Screenshot From 2025-11-14 10-29-08" src="https://github.com/user-attachments/assets/56aba5dc-ee51-4a53-8261-2eaf6c1f144c" />


<img width="808" height="750" alt="Screenshot From 2025-11-14 10-26-17" src="https://github.com/user-attachments/assets/1d05a84f-62ae-4e09-a0a4-5d5b40dc818a" />

Caddyn asentaminen onnistui!


```
sudo systemctl stop apache2
sudo systemctl restart caddy
joonas@Joonasdebian:~$ sudo systemctl status caddy
```

Annetaan oikeudet tavallisille kayttajalle:

```
whoami
sudo chown -R joonas:joonas /var/www/html
sudo chmod -R 755 /var/www/html
nano /var/www/html/index.html
```

Yhteenvetona:
Tavallinen käyttäjä voi muokata tiedostoa, kunhan hänellä on oikeudet kirjoittaa tiedostoon ja hakemistoon.
Omistajuuden muuttaminen omalle käyttäjälle tai oikeuksien säätäminen (kuten chmod 755) mahdollistaa muokkaamisen ilman sudo-oikeuksia.


<img width="900" height="332" alt="Screenshot From 2025-11-14 11-11-59" src="https://github.com/user-attachments/assets/7241cf4b-7c72-42cb-9926-5c2465e7aa5e" />


###### 11:14
Tauko
###### 11:25

d) Vapaaehtoinen, haastava: Nginx. Asenna Nginx (lausutaan engine-X) tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.

Nginx asennus:

```
sudo apt update
sudo apt install nginx
```

Konfugorointi:

```
mkdir -p /home/joonas/public_html
```

Annetaan oikeudet toimia ilman sudoa. Tama mahdollistaa tiedostojen muokkaamisen, ilman sudo - oikeuksia.

```
sudo chown -R joonas:joonas /home/joonas/public_html
chmod -R 755 /home/joonas/public_html
mkdir -p ~/public_html
echo "<h1>Hello World! Tervetuloa</h1>" > ~/public_html/index.html
```
Oikeudet ja luvat:
```
sudo chown -R joonas:joonas ~/public_html
chmod 711 /home/joonas
chmod 755 ~/public_html
chmod 644 ~/public_html/index.html
```

Nginx - sivujen konfigurointi:
```
sudo nano /etc/nginx/sites-available/homepage
```
Caddy poistettiin portista 80, ja tehtiin seuraavanlainen muutos:

```
server {
    listen 80;
    server_name localhost;

    root /home/joonas/public_html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

```
sudo ln -s /etc/nginx/sites-available/homepage /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default   # Poista oletussivusto
```

Testaminen suoritettiin onnistuneesti!

```
sudo nginx -t
sudo systemctl restart nginx
```


<img width="807" height="386" alt="Screenshot From 2025-11-14 12-25-17" src="https://github.com/user-attachments/assets/373656a8-fcbc-4b2c-9df3-b4c5dd93f548" />


Yhteenveto:

###### 12:29 
###### 12:33
e) Vapaaehtoinen, haastava: PostgreSQL. Asenna PostgreSQL-tietokannanhallintajärjestelmä. Anna jollekin käyttäjälle oma tietokanta. Osoita testillä, että se toimii.

```
sudo apt update
sudo apt install postgresql postgresql-contrib -y
```
```
sudo -i -u postgres
psql
```
```
CREATE USER myuser WITH PASSWORD 'mypassword';

CREATE DATABASE mydb OWNER myuser;

GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;

GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;

\q

```

Tyhjensin tiedoston, ja sisallytin nama sinne:

local   all             all                                     md5
host    all             all             127.0.0.1/32            md5
host    all             all             ::1/128                 md5


<img width="806" height="223" alt="Screenshot From 2025-11-14 12-52-17" src="https://github.com/user-attachments/assets/f53084ce-503b-4393-b127-06cb13569e94" />

Testi

Osoitetaan testilla, etta toimii:

<img width="960" height="536" alt="Screenshot From 2025-11-14 13-01-13" src="https://github.com/user-attachments/assets/28e7a64e-cf9d-41fe-8cb0-33ff1469376a" />


Asentamisen jalkeen: Tietokannanhallintajärjestelmä (PostgreSQL) asennettiin koneelle, jotta voidaan käyttää relaatiotietokantaa.
Luotiin uusi käyttäjä.PostgreSQL:ään lisättiin käyttäjä (esim. CREATE USER nimi WITH PASSWORD 'salasana';). Tämä käyttäjä sai omat tunnukset tietokantaan. Annettiin käyttäjälle oma tietokanta. Luotiin uusi tietokanta (esim. CREATE DATABASE kayttaja_db OWNER nimi;). Käyttäjä sai oikeudet hallita juuri tätä tietokantaa. Testattiin toimivuus. Kirjauduttiin sisään kyseisen käyttäjän tunnuksilla. Suoritettiin yksinkertainen testi, esim. taulun luonti ja rivin lisääminen (CREATE TABLE, INSERT, SELECT).

###### 13 :12 

Kaikki tehtavat olivat haastavia. Voi olla, etta virheita on tehtavissa.




Lähteet 
-----

CaddyServer 2025. Install. Luettavissa: https://caddyserver.com/docs/install. Luettu: 14.11.2025.

GitHub 2025. Joonas Janttonen. Laksyt. Luettavissa: https://github.com/JoonasJanttonen/Palvelinten-hallinta/edit/main/h3%20Soitto%20kotiin.md. Luettu: 12.11.2025.

Microfocus 2025. Luettavissa: https://www.microfocus.com/documentation/idol/IDOL_12_0/MediaServer/Guides/html/English/Content/Getting_Started/Configure/_TRN_Set_up_PostgreSQL_Linux.htm. Luettu: 14.11.2025.

Tero Karvinen 2025. Palvelinten hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt. Luettu: 12.11.2025.

Tero Karvinen 2018. Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh. Luettu: 12.11.2025.

Tero Karvinen 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Luettu: 12.11.2025.

Wikipedia 13.11.2025. PostgreSQL. Luettavissa: https://fi.wikipedia.org/wiki/PostgreSQL. Luettu: 14.11.2025.
