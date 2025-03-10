---

---

# h6 Salataampa





## x)



#### Let's Encrypt 2024: [How It Works](https://letsencrypt.org/how-it-works/)

****Tavoite**: Mahdollistaa HTTPS-palvelimen automaattinen varmenteen hankinta ilman ihmisen väliintuloa.

**Toimintaperiaate**: Palvelimella ajetaan varmenteenhallintaohjelmisto, joka hoitaa domainin validoinnin, varmenteen haun, uusimisen ja perumisen.

**Domainin validointi**: Palvelin todistaa hallitsevansa domainia joko:

- Lisäämällä DNS-tietueen, tai
- Luomalla tietyn tiedoston palvelimelle Let’s Encryptin määrittämään osoitteeseen.

**Varmenteen myöntäminen**: Kun domainin hallinta on todistettu, CA (Certificate Authority) myöntää varmenteen.

**Varmenteen uusiminen ja peruminen**:

- Uusiminen tapahtuu automaatisesti samoilla tunnistetiedoilla.
- Peruminen (eng. revocation) tehdään allekirjoitetulla pyynnöllä, minkä jälkeen selain ei enää luota varmenteeseen.

**Turvallisuus**: Varmenteet ja niiden hallinta perustuvat kryptografisiin allekirjoituksiin, ja tiedot tallennetaan julkisiin Certificate Transparency (CT) -lokeihin.



#### Lange 2024: Lego: Obtain a Certificate: [Using an existing, running web server](https://go-acme.github.io/lego/usage/cli/obtain-a-certificate/index.html#using-an-existing-running-web-server)

- Jos webpalvelin on jo käynnissä portissa 80, **--http**-vaihtoehto vaatii **--http.webroot**-valinnan, joka tallentaa haasteen **.well-known/acme-challenge**-kansioon ilman että se käynnistää uutta palvelinta.

- Tämä kansio pitää olla julkisesti saatavilla domainilla, muuten täytyy tehdä uudelleenkirjoitussääntö (rewrite).

- Esimerkki Let’s Encrypt -varmenteen hankinnasta:

  ```shell
  lego --accept-tos --email you@example.com --http --http.webroot /polku/webrootiin --domains example.com run
  ```

- `Skriptin` voi ajaa automaattisesti varmenteen haun jälkeen 

  --run-hook

  -vaihtoehdolla:

  ```sh
  lego --email="you@example.com" --domains="example.com" --http run --run-hook="./myscript.sh"
  ```

- Ympäristömuuttujista saa tietoa mm. varmenteen sijainnista ja domainista (**LEGO_CERT_PATH**, **LEGO_CERT_DOMAIN**, jne.).



#### The Apache Software Foundation 2025: Apache HTTP Server Version 2.4 [Official] Documentation: SSL/TLS Strong Encryption: How-To: [Basic Configuration Example](https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample)

- SSL-konfiguraation perusasetukset vaativat **mod_ssl**-moduulin lataamisen.
- Palvelin kuuntelee liikennettä portissa **443** (HTTPS).
- **VirtualHost**-lohko määrittää domainin (ServerName) ja ottaa SSL-salauksen käyttöön.
- Varmenteen ja avaimen sijainnit määritellään direktiiveillä **SSLCertificateFile**





## Tehtävänä siis salata webbipalvelin ja hankkia certit

#### Virtuaalikoneen tiedot

![h60](F:/h6/h60.png)

Ensimmäisenä ajoin 

`sudo apt update && sudo apt upgrade`

sitten avaan portin 443 tcp protokollalle:

`sudo ufw allow 443/tcp`

![image-20250309223543782](C:\Users\Jerep\AppData\Roaming\Typora\typora-user-images\image-20250309223543782.png)



Sitten asennan lego:n

`sudo apt install lego`

![image-20250309223118566](C:\Users\Jerep\AppData\Roaming\Typora\typora-user-images\image-20250309223118566.png)

Avasin ja muokkasin /etc/apache2/sites-available/jerepellinen.com.conf -tiedostoa

![image-20250310024757369](C:/Users/Jerep/AppData/Roaming/Typora/typora-user-images/image-20250310024757369.png)



Hain keyt cloudfaresta

![image-20250310024458492](C:/Users/Jerep/AppData/Roaming/Typora/typora-user-images/image-20250310024458492.png)

Kopion nämä keyt /home/jere/public_sites/jerepellinen.com/certificates -kansioon

![image-20250310025059796](F:/h6/h65.png)



![image-20250310025153817](C:/Users/Jerep/AppData/Roaming/Typora/typora-user-images/image-20250310025153817.png)

Käynnistin apache 2 uudelleen.

`sudo systemctl stop apache2`

`sudo systemctl start apache2`

sain cloudfaresta ssl keyn ja pem:in.



Sivustoni ei oikein toimi enää. yhtäkkiä siellä lukee torstai ton toivoa täynnä. En tiiä mikä meni pipariksi. Pakko mennä nukkumaan. Pitää herätä töihin 2.5h päästä. Eli en ehtinyt enempää. Harmittaa kun tämä on niin mielenkiintoista :/



**Lähteet:**

ssl toiminta: [Cloudflare origin CA · Cloudflare SSL/TLS docs](https://developers.cloudflare.com/ssl/origin-configuration/origin-ca/)

Tehtävän anto ja hyviä vinkkejä [Linux Palvelimet 2025 alkukevät - ICI003AS2A-3008 +lp](https://terokarvinen.com/linux-palvelimet/)

Selkeää selitystä miten ssl toimii [How It Works - Let's Encrypt](https://letsencrypt.org/how-it-works/)

Hyviä neuvoja vaikken käyttänyt ja olisi kannatytanut kyllä[Obtain a Certificate :: Let’s Encrypt client and ACME library written in Go.](https://go-acme.github.io/lego/usage/cli/obtain-a-certificate/index.html#using-an-existing-running-web-server)

Joni Laine henkisestä tuesta <3

Hyvää documentaatiota https://upcloud.com/resources/ 