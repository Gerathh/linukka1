

```md
# H3 Hello Web Server

[Apache HTTP Server Documentation: Name-Based Virtual Hosts](https://httpd.apache.org/docs/2.4/vhosts/name-based.html)  
- IP-pohjaisessa jokaiselle verkkotunnukselle tarvitaan oma IP-osoite.  
- Nimipohjaisessa samaa IP-osoitetta voidaan käyttää useille verkkotunnuksille.  
- Jos käyttäjän pyyntö ei vastaa mitään tiettyä **ServerName** tai **Alias** -määritystä, niin käytetään ensimmäistä VirtualHostia, joka vastaa IP:hen ja porttiin; eli ensimmäinen VirtualHost toimii oletuspalveluna.

[Name-based Virtual Hosts on Apache (Terokarvinen.com)](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/)  
- Sivulla kerrotaan hyvin, miten yhdellä IP-osoitteella voidaan ajaa useita verkkotunnuksia Apachen avulla.  
- Käytännössä konfiguraatio tehdään luomalla jokaista verkkotunnusta varten oma VirtualHost-asetus.  
  - Määritellään **ServerName**, **ServerAlias** ja **DocumentRoot**.  
- Tiedostossa `/etc/apache2/sites-available/` säilytetään sivuston konfiguraatio.  
  - Tämän jälkeen sivusto aktivoidaan komennolla `a2ensite` ja Apache käynnistetään uudelleen.

---

## a) Localhost vastaa

![Localhost vastaa](https://raw.githubusercontent.com/Gerathh/linukka1/main/h31.png)

---

## b) Lokitiedoston katsominen

Annoin käskyt:

```bash
cd /
sudo nano /var/log/apache2/access.log
```

1. **IP-osoite** (localhost = 127.0.0.1).  
2. **Viiva** (ident-kenttä) – ident-tietoa ei käytetä.  
3. **Toinen viiva** (autentikoitu käyttäjä -kenttä) – jos olisi perusautentikointi tms., käyttäjätunnus näkyisi tässä.  
4. **Aikaleima** (päivä, kellonaika, aikavyöhyke).  
5. **Pyynnön sisältö**  
   - Esim. `GET /index.html HTTP/1.1`  
   - `GET` on HTTP-metodi  
   - `/index.html` pyydetty URL-polku  
   - `HTTP/1.1` protokollan versio  
6. **HTTP-vastauskoodi** (esim. `200` = OK).  
   - (404 yleinen, jos sivua ei löydy)  
7. **Tiedoston koko** tavuina.  
8. **“-”** – jos olisi klikattu linkkiä toiselta sivulta, tähän tulisi sen URL.  
9. **Asiakkaan tunniste** (selaimen user-agent) – kertoo esim. käyttöjärjestelmän ja selaimen.

---

## c) VirtualHost-määrityksen lisääminen

Annoin seuraavat käskyt:

```bash
cd /
ls etc/apache2/sites-available/
sudo a2dissite 000-default.conf
sudo nano /etc/apache2/sites-available/hattu.example.com.conf
```

Lisäsin tiedostoon esimerkiksi seuraavan sisällön:

```apache
<VirtualHost *:80>
    ServerName hattu.example.com
    ServerAlias localhost
    DocumentRoot /home/jere/hattu
    <Directory /home/jere/hattu>
        Require all granted
    </Directory>
</VirtualHost>
```

- **ServerName**: pääverkkotunnus, jota VirtualHost palvelee  
- **ServerAlias**: mahdollistaa sisällön näkymisen myös `http://localhost/` -osoitteessa  
- **DocumentRoot**: osoittaa yllä luotuun kansioon  
- `<Directory>`-määritys: sallii tehtävänannon mukaisesti kaikille pääsyn sisältöön

Seuraavaksi:

```bash
sudo a2ensite etc/apache2/sites-available/hattu.example.com.conf
```

Sain virheilmoituksen:

```
ERROR: Site /etc/apache2/sites-available/hattu.example.com does not exist!
```

Polussa oli ongelma. Kokeilin:

```bash
cd /etc/apache2/sites-available/
sudo a2ensite hattu.example.com.conf
```

Ilmoitus: `Enabling site hattu.example.com`. Apache2 tulee vielä käynnistää uudelleen tai ladata asetukset uudelleen:

```bash
systemctl reload apache2
```

`curl http://localhost` näyttää sisällön, mutta selain ei. `curl hattu.example.com` toimii. Luin Apachen oletussivuja ja päätin sallia `/home/jere/` -hakemistossa web-selauksen:

```bash
sudo nano /etc/apache2/apache2.conf
```

Lisäsin sinne:

```
<Directory /home/jere/>
    Require all granted
</Directory>
```

(jos se ei jo ollut määritelty VirtualHost-asetuksessa).

Nyt kaikki toimii. 😊

---

## Lähteet

- [Apache HTTPD 2.4 Name-based Virtual Hosts Documentation](https://httpd.apache.org/docs/2.4/vhosts/name-based.html)  
- [Name-based Virtual Hosts on Apache (Terokarvinen.com)](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/)
```
