# Maailma kuulee

x\)

- Kirjoittaja vuokrasi DigitalOceanilta virtuaalipalvelimen ja liitti siihen Namecheapilta hankitun domain-nimen GitHub Student Developer Pack -etujen avulla.

- Palvelimelle asennettiin Debian 11, peruskonfigurointi (SSH, uusi käyttäjä, root-käyttäjän lukitus) ja ufw-palomuuri.

- Apache-webpalvelin otettiin käyttöön, testisivu korvattiin omalla sivulla ja käyttäjän kotihakemistoon luotiin public_html-hakemisto.

- Lokitiedoista löytyi merkkejä automaattisista murtautumisyrityksistä, jotka kariutuivat vahvan salasanan ja turvallisuusasetusten ansiosta.

x\)

- Artikkelissa opastetaab uuden virtuaalipalvelimen (DigitalOcean + Ubuntu 16.04 LTS) peruskonfiguroinnissa ja varmistetaan, että käyttäjä käyttää vain vahvoja salasanoja.

- Ensimmäisiin toimiin kuuluvat uuden käyttäjän luominen (root-käytön minimointi), palomuurin määrittäminen (ufw) sekä turhat pääkäyttäjäyhteydet estävä root-tunnuksen lukitseminen.

- Järjestelmä on aina syytä päivittää (apt-get update/upgrade) heti tietoturvan varmistamiseksi.

- Domain-nimen (NameCheap) yhdistäminen IP-osoitteeseen mahdollistaa julkisille verkkopalveluille helpommin muistettavan osoitteen.





## a)  Vuokrasin Palvelimen UpCloud.com:sta

 

Valitsin rekisteröidyttyäni sekä luottokorttitietojen anstamisen jälkeen Deploy server

![h41](https://github.com/Gerathh/linukka1/blob/main/h41.png)

Valitsin sijainniksi Suomen.  1Core, 1GB ram, 10GB tallennustilaa.



![h42](https://github.com/Gerathh/linukka1/blob/main/h42.png)

Valitsin käyttöjärjestelmäksi Debian GNU/Linux 12 (Bookworm)

![h43](https://github.com/Gerathh/linukka1/blob/main/h43.png)

Laitoin deploy. 



Tämän jälkeen siirryin virtuaalikoneelle. Kuvassa näkyy, että open-ssh on asennettuna.



![h44](https://github.com/Gerathh/linukka1/blob/main/h44.png)

ssh-keygen komennolla sain luotua public keyn. Jätin passwordin tyhjäksi enterillä.



![h45](https://github.com/Gerathh/linukka1/blob/main/h45.png))

komennnolla:

`cat id_rsa.pub`

![h46](https://github.com/Gerathh/linukka1/blob/main/h46.png)

Sain tulostettua public keyn jonka copy-pastesin upcloudiin ssh keyksi ja painoin siellä deploy.



## b)

Ucloudin ohjeiden mukaan "How to connnect " laitoin komennon

`ssh root@94.237.32.234`

Tämän jälkeen kirjoitin yes (pelkkä y ei kelpaa, jota automaagisesti kokeilin)

![h47](https://github.com/Gerathh/linukka1/blob/main/h47.png)

Ajoin komennot

`sudo apt update`

`sudo apt upgrade`

Sitten lisäsin käyttäjän

`sudo adduser jere`

jonka jälkeen

`sudo adduser jere sudo`

![h48](https://github.com/Gerathh/linukka1/blob/main/h48.png)

Tämän jälkeen ansensin vielä roottina micron:

`apt install micro`

Tämän jälkeen menin kansioon /root/.ssh/ ja varmistin että siellä on key.

Sitten menin kansioon /home/jere/

Kopioin komennolla

`cp -n -r /root/.ssh /home/jere/`

kaikki sisällöt jeren kansioon.

Tämän lisäksi kopioin ne vielä petterin kansioon.

suoritin sitten komennon

`chow jere.jere .ssh -R`

![h410](https://github.com/Gerathh/linukka1/blob/main/h410.png)

tämän jälkeen poistuin kirjoittamalla

`exit`

sen jälkeen kirjoitin

ssh jere@94.237.32.234

ja olin nyt sisällä käyttäjänä enkä roottina

![h411](https://github.com/Gerathh/linukka1/blob/main/h411.png)

Varmistin että käyttäjälläni on sudot. ja sitten poistin rootin käytöstä.

`sudo echo Terve`

`sudo usermod --lock root`

`sudo rm /root/.ssh -r`

![h412](https://github.com/Gerathh/linukka1/blob/main/h412.png)

Seuraavaksi palomuuri päälle

`sudo apt install ufw`

`sudo ufw allow ssh`

`sudo ufw allow http`

`sudo ufw allow https`

`sudo ufw enable`

ja tarkistetaan vielä että se on päälllä varmasti

`sudo ufw status verbose`

![h413](https://github.com/Gerathh/linukka1/blob/main/h413.png)

Selaimeen IP jolla todennan että se on pystyssä ja toimii:

![h414](https://github.com/Gerathh/linukka1/blob/main/h414.png)

## c)

Tämän jälkeen:

`echo moi torstai on toivoa täynnä | sudo tee /var/www/html/index.html`



![h415](https://github.com/Gerathh/linukka1/blob/main/h415.png)



  Lähteet: https://terokarvinen.com/linux-palvelimet/
https://hub.upcloud.com/
https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/
Joni Ikolainen
