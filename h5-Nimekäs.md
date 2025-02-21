# H5 - Nimekäs

## a)

Minulla on  olemassa oleva dooimain jerepellinen.com jonka tiedostot sijaitsevat githubissa.



Aloitin dns -palvelintarjoajalta jolta olen domainin vuokrannut/hankkkinut eli cloudfare.com:ista Muutin aiemmat tiedot alla olevan kuvan mukaiseksi. 

UpCloudissta vuokraamani palvelimen ip on `94.237.32.234`

![h51](https://github.com/Gerathh/linukka1/blob/main/h51.png)




Tämän jälkeen kirjauduin virtuaaallipalvelimelle. Olen aiemmmin luonut käyttäjän nimeltä testi jolla ei ole sudo-oikeuksia. (tapahtuu käyttäjällä jolla on sudo-oikeudet ja kirjoittamallla

 `sudo adduser testi` ja antamalla tapelliset tiedot ja salasanat sille selkeiden konsoilissa olevien ohjeiden mukaisesti.

Annoin sitten seuraavat käskyt:

`sudo mkdir -p /var/www/jerepellinen.com`

`sudo chown -R testi:testi/var/www/jerepellinen.com`

`sudo chmod -R 755 /var/www/jerepellinen.com`



![h52](https://github.com/Gerathh/linukka1/blob/main/h51.png)



------

## b)



Sen jälkeen loin conffaustiedoston jerepellinen.com:lile

`sudo nano /etc/apache2/sites-available/jerepellinen.conf`



Lisäsin sinne kuvan mukaiset rivit:

![h53](F:\h5\h53.png)

annoin komennot:

sudo a2ensite jerepellinen.conf
sudo systemctl reload apache2

tuli error.

Ehdotti katsomaan journalctl -xeu ja sieltähän se virhe löytyi. Näkyy myös ylläolevassa kuvassa.

![h54](F:\h5\h54.png)

Korjasin tiedoston ja suoritin aiemmat komennot uudestaan.



Sitten varmistin vielä palomuuria seuraavilla komennoilla

Kävin vielä tarkistamassa ,

`sudo nano /etc/ufw/applications.d/ufw-webserver`

että palomuurissa on tarvittavat portit auki.

![h55](F:\h5\h55.png)





## c)



Tiedostojen kopiointi jo olemassa olevalta palvelimelta (github)



`cd /var/www/`

`sudo apt install git`

`sudo git clone https://github.com/Gerathh/jerepellinen.com.git jerepellinen.com`

Oikeudet kuntoon:

`sudo chown -R testi:testi /var/www/jerepellinen.com`

![h56](F:\h5\h56.png)

Muokkasin jerepellinen.conf -tiedostoa lisäämällä sinne alidomainit.

![h57](F:\h5\h57.png)

Sitten vielä komento

`sudo systemctl reload apache2`

## e)



`sudo apt update`
`sudo apt install dnsutils`

`host -v jerepellinen.com` näyttää hyvin kyselyn tuloksia. dns palvelimen. ja IP -osoitteen josta tiedot tulevat.

`host linuxkurssi.jerepellinen.com` andtaaa palvelimen IP:n.

`host test.jerepellinen.com` Tämä on CNAME jolloin tuloksessa näkyy myös että tämä on alias.

![h58](F:\h5\h58.png)



`host google.com` näyttäää IPv4 osoitteen, IPv6 osoitteen sekä googlen sähköpostipalvelimen osoitteen



















https://unix.stackexchange.com/questions/460480/allow-access-to-apache-on-both-port-80-and-443-in-ubuntu-16-04

https://www.linux.org/threads/solved-failed-to-start-the-apache-http-server.39105/

[django - How do I create add a domain's configuration file to /etc/apache2/sites-available/ in Apache2? - Stack Overflow](https://stackoverflow.com/questions/63527186/how-do-i-create-add-a-domains-configuration-file-to-etc-apache2-sites-availabl)

[Rename a File in Linux – Bash Terminal Command](https://www.freecodecamp.org/news/rename-file-linux-bash-command/)
