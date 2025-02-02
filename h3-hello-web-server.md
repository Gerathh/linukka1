# Hello Web Server

### x)
https://httpd.apache.org/docs/2.4/vhosts/name-based.html  
• IP- pohjaisessa jokaiselle verkkotunnukselle tarvitaan oma IP-osoite  
• Nimipohjaisessa samaa UIP-osoitetta voidaan käyttää useille verkkotunnuksille  
• Jos käyttäjän pyyntö ei vastaa mitään tiettyä ServerNamke taI Alias-määritystä, niin käytetään ensimmmäistä Virtualhostia joka vastaa IP:hen ja porttiin; eli ensimmäinen virtualHost toimii oletuspallveluna.

https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/  

• Sivulla kerrotaan hyviun miten yhdellä IP-osoitteella voidaan ajaa useita verkkotunnuksia Apachen avulla  
• Käytännössä confaus tehdään luomalla jokaista verkkotunnusta varten oma VirtualHost-asetu. Siinä määäritellään ServerName, ServerAlias ja DOcumentRoot  
• Tiedostossa `/etc/apache2/sites-available/` säilytetään sivuston konfiguraatio. Tämän jälkeen sivusto aktivoidaan komennolla `a2ensite` ja Apache käynnistetään uudelleen.

### a)
Localhost vastaa

![h31.png](https://github.com/Gerathh/linukka1/blob/main/h31.png)

### b)
Annoin käskyt

```bash
cd /
sudo nano /var/log/apache2/access.log
```

![h32.png](https://github.com/Gerathh/linukka1/blob/main/h32.png)

• Ensimmäisenä on IP osoite, josta pyyntö tuli. (localhost=127.0.0.1)  
• Sitten on viiva joka tarkoittaa ident -kenttää. Viiva kertoo että ident -tietoa ei käytetä.  
• Toinen viiva on autentikoitu käyttäjä-kenttä- Jos Apacheen olisi määritelty perusautentikointi, tai joku muu tunnistautuminen ja se olisi onnistunut, näkyisi tässä käyttäjätunnus.  
• Seuraavana aikaleima milloin pyyntö on saatu. Päivä, kellonaika ja aikavyöhyke  
• Seuraavana esim. kuvassa oleva rivi: `GET /index.html HTTP/1.1` kertoo http-metodin, pyydetyn URL-polun ja http-protokollan version  
• 200 http-palvelimen vastauskoodi.  
  o 200 = OK eli pyyntö onnistunut  
  o (404 on aika yleinen, jos sivustoa ei löydy)  
• Tiedoston koko tavuina  
• `"-"` tarkoittaa, että jos käyttäjä olisi klikannut linkkiä toiselta sivulta, tulisi sen URL tähän  
• Viimeisenä asiakkaan tunniste, josta voidaan päätellä, että pyyntö tuli Linuxista ja mozilla firefox -selaimella.

### c) d) e) f)
Annoin seuraavat käskyt

```bash
cd /
ls etc/apache2/sites-available/
sudo a2dissite 000-default.conf
sudo nano /etc/apache2/sites-available/hattu.example.com.conf
```

Lisäsin sinne seuraavan sisällön:

![h33.png](https://github.com/Gerathh/linukka1/blob/main/h33.png)

• `ServerName` on pääverkkotunnus, jota tämä VirtualHost palvelee  
• `ServerAlias localhost` sallii saman sisällön näkymisen myös osoitteessa [http://localhost/](http://localhost/)  
• `DocumentRoot` osoittaa kansioon, jonka loin yllä  
• `<Directory>`-määrityksessä sallitaan tehtävänannon mukaisesti kaikille pääsy sisältöön

Annoin sitten seuraavan komennon:

```bash
sudo a2ensite etc/apache2/sites-available/hattu.example.com.conf
```

Sain virheilmoituksen  
“ERROR: Site /etc/apache2/sites-available/hattu.example.com does not exist!”  
Eli pitää vähän vielä säätää.

```bash
cd /
sudo nano /etc/hosts
```

Muunsin ensimmäisen rivin muotoon `127.0.0.1 hattu.example.com`

![h34.png](https://github.com/Gerathh/linukka1/blob/main/h34.png)

Nyt uudestaan sama komennon:

```bash
sudo a2ensite etc/apache2/sites-available/hattu.example.com.conf
```

No, ei toimi vieläkään. Sama virheilmoitus. Ehkä minun pitää olla samassa hakemistossa?

```bash
cd /etc/apache2/sites-available/
sudo a2ensite hattu.example.com.conf
```

![h35.png](https://github.com/Gerathh/linukka1/blob/main/h35.png)

Nyt tuli miellyttävämpi ilmoitus, kuten kuvasta näkyy:  
"Enabling site hattu.example.com."  
Vielä muistutan, että käynnistetään Apache uudestaan. Joten:

```bash
Systemctl reload apache 2
```

Curlilla näkee [http://localhost](http://localhost) sisällön, mutta ei selaimella. Sen lisäksi Curlilla näkee hattu.example.com. Kyse on siis jostain muusta. Lueskeltuani Apachen oletus-etusivua, päätän mennä whitelistaamaan hakemiston, missä tiedosto sijaitsee.

```bash
sudo nano /etc/apache2/apache2.conf
```

Sinne lisäsin hakemiston whitelistille myös `/home/jere/` ja `Require all granted`, jonka olen laittanut aiemmin tiedostoon `hattu.example.com.conf`.

![h36.png](https://github.com/Gerathh/linukka1/blob/main/h36.png)

No nyt pelittää 😊

![H37.png](https://github.com/Gerathh/linukka1/blob/main/h37.png)

Lähteenä Apachen oletus-etusivu (ensimmäinen kuva)  
https://httpd.apache.org/docs/2.4/vhosts/name-based.html  
https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/

---

**Tekijä**: Jere Pellinen, Haaga-Helian ammattikorkeakoulu, Tradenomi (AMK), tietojenkäsittely opiskelija
**Helsinki, 2025**
