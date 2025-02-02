```md
# H3 Hello Web Server

[Apache HTTP Server Documentation: Name-Based Virtual Hosts](https://httpd.apache.org/docs/2.4/vhosts/name-based.html)  
- IP-pohjaisessa jokaiselle verkkotunnukselle tarvitaan oma IP-osoite  
- Nimipohjaisessa samaa IP-osoitetta voidaan käyttää useille verkkotunnuksille  
- Jos käyttäjän pyyntö ei vastaa mitään tiettyä **ServerName** tai **Alias** -määritystä, niin käytetään ensimmäistä VirtualHostia, joka vastaa IP:hen ja porttiin; eli ensimmäinen VirtualHost toimii oletuspalveluna.

[Name-based Virtual Hosts on Apache (terokarvinen.com)](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/)  
- Sivulla kerrotaan hyvin, miten yhdellä IP-osoitteella voidaan ajaa useita verkkotunnuksia Apachen avulla.  
- Käytännössä konfiguraatio tehdään luomalla jokaista verkkotunnusta varten oma VirtualHost-asetus. Siinä määritellään **ServerName**, **ServerAlias** ja **DocumentRoot**.  
- Tiedostossa `/etc/apache2/sites-available/` säilytetään sivuston konfiguraatio. Tämän jälkeen sivusto aktivoidaan komennolla `a2ensite` ja Apache käynnistetään uudelleen.

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

- Ensimmäisenä on IP-osoite, josta pyyntö tuli (localhost=127.0.0.1).  
- Sitten on viiva, joka tarkoittaa ident-kenttää. Viiva kertoo, että ident-tietoa ei käytetä.  
- Toinen viiva on autentikoitu käyttäjä -kenttä. Jos Apacheen olisi määritelty perusautentikointi tai joku muu tunnistautuminen ja se olisi onnistunut, näkyisi tässä käyttäjätunnus.  
- Seuraavana aikaleima, milloin pyyntö on saatu: päivä, kellonaika ja aikavyöhyke.  
- Seuraavana esim. kuvassa oleva rivi: `GET` on HTTP-metodi, `/index.html` on pyydetty URL-polku, `HTTP/1.1` kertoo HTTP-protokollan version.  
- `200` on HTTP-palvelimen vastauskoodi.  
  - 200 = OK eli pyyntö onnistunut  
  - (404 on yleinen, jos sivua ei löydy)  
- Tiedoston koko tavuina.  
- `"-"` tarkoittaa, että jos käyttäjä olisi klikannut linkkiä toiselta sivulta, tähän tulisi sen URL.  
- Viimeisenä asiakkaan tunniste, josta voidaan päätellä että Linuxista tullut ja Mozilla Firefox -selaimella.

---

## c) VirtualHost-määrityksen lisääminen

Annoin seuraavat käskyt:

```bash
cd /
ls etc/apache2/sites-available/
sudo a2dissite 000-default.conf
sudo nano /etc/apache2/sites-available/hattu.example.com.conf
```

Lisäsin tiedostoon seuraavan sisällön (esimerkkinä):

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

- **ServerName** on pääverkkotunnus, jota tämä VirtualHost palvelee.  
- **ServerAlias** localhost sallii saman sisällön näkyvän myös osoitteessa `http://localhost/`.  
- **DocumentRoot** osoittaa kansioon, jonka loin yllä.  
- `<Directory>` -määrityksessä sallitaan tehtävänannon mukaisesti kaikille pääsy sisältöön.

Seuraavaksi komennot:

```bash
sudo a2ensite etc/apache2/sites-available/hattu.example.com.conf
```

Sain virheilmoituksen:

```
ERROR: Site /etc/apache2/sites-available/hattu.example.com does not exist!
```

Eli polussa oli ongelma. Kokeilin ensin siirtyä samaan hakemistoon:

```bash
cd /etc/apache2/sites-available/
sudo a2ensite hattu.example.com.conf
```

Nyt tuli miellyttävämpi ilmoitus: `Enabling site hattu.example.com`. Vielä muistuttaa, että käynnistä Apache2 uudestaan. Joten:

```bash
systemctl reload apache2
```

`curl`-komennolla näkee `http://localhost`in sisällön, mutta ei selaimella. `curl`illa näkee myös `hattu.example.com`. Kyse on siis jostain muusta. Lueskeltuani Apachen oletus-etusivua, päätin mennä whitelistaamaan hakemiston, missä tiedosto sijaitsee:

```bash
sudo nano /etc/apache2/apache2.conf
```

Sinne lisäsin hakemiston whitelistille myös `/home/jere/` ja `Require all granted`, jonka olin laittanut aiemmin tiedostoon `hattu.example.com.conf`.

Nyt kaikki pelittää. 😊

---

## Lähteet

- [Apache HTTPD 2.4 Name-based Virtual Hosts Documentation](https://httpd.apache.org/docs/2.4/vhosts/name-based.html)  
- [Name-based Virtual Hosts on Apache (terokarvinen.com)](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/)
```
