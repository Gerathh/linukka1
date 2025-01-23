# H2 tehtävä Komentaja Pingviini

## x) Lue ja tiivistä

-   Kemontorivi on ollut olemassa enne Googlea, Webbiä, Linuxia,
    Windowsia ja jopa ennen Internettiä.

-   Nämä komennot ovat peruskometoja joita tarvitsee joka päivä kun on
    Linuxin kanssa tekemisisssä joten nämä ao. linkistä löytyvät
    peruskäskyt on tärkeää painaa mieleen.
    <https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited>

-   Tärkeitä kansioita on / , /home /, /home/Username/ , /etc/ , /media/
    , /var/log/ Näistäkin selitykset löytyvät englanniksi yo linkistä.

-   Sudo on äärimmäisen tärkeä komento ylläpitäjälle tai
    yksityiskoneelle jos haluat asentaa ohjelmia. En antaisi vaarilleni.
    Jos käyttäjäsi kuuluu sudo-ryhmään, niin saat sillä suoritettua
    vaikkapa kernelin päivityksen tai asennettua ohjelmia.

*Rauta*

<https://github.com/Gerathh/linukka1/blob/main/win2.png>

*Virtuaalikoneen tiedot ja versiot*

### <https://github.com/Gerathh/linukka1/blob/main/virtuaalikoneentiedot.png>

### Aika 0:00

## *Koneen avaus*

-   Boottasin koneen painamalla start

-   Hetken päästä OS kysyi käyttäjänimeä ja salasanaa, jotka laitoin

-   Avasin terminaalin ja kirjoitin **sudo apt update** jonka jälkeen
    **sudo apt upgrade** ja enteriä

## Micro

-   Annoin alla olevan komennon ja painoin enter

### 

### Aika 0:07

## b) Apt

-   Annoin seuraavan käskyn

    -   **sudo apt update && sudo apt install -y htop tree ncdu**

        -   kysyi salasanaa, kirjoitin sen ja painoin enteriä.

        -   && tekee sen, että jälkimmäinen ajetaan vain, jos
            ensimmäinen onnistuu

        -   -y Tekee sen, että se laittaa automaattisesti yes jokaisen
            kohdalla.

<https://github.com/Gerathh/linukka1/blob/main/ter3asen.png>

Aika 0:18

## c) FHS

### Aika 1:30

### d) The Friendly M ja e) Pipe

grep on monipuolinen.

Käskyllä

grep hakee ja listaa rivit, joilta löytyy merkkijono "virhe" tiedostosta
syslog

Käskyllä

-r eli rekursiivinen haku, käy läpi kaikki alihakemistot ja niiden
tiedostot annetussa polussa, tässä tapauksessa projektit, ja etsiii
sieltä merkkijonoa "Kiire". Sen jälkeen se tulostaa kaikki rivit, joissa
näkyy tämä hakusana sekä niiden tiedoston nimet.

Putkittaminen ja grep

ps aux listaa kaikki käynnissä olevat prosessit. Lisätään \| grep "jere"
niin se hakee näistä käynnissä olevista tehtävistä kaikki, jotka
sisältävät tekstin "jere". Lisätään vielä \| nl niin saadaan
järjestysnumerot listauksen eteen. Lisäsin vielä \| less tuohon eteen
niin se antaa niin paljon vastauksia, kun terminaaliin mahtuu kerralla,
ja voit kelata ylös ja alas nuolilla ylös ja alaspäin. Hiiren rullakin
toimii.

### Aika 1:46

### f) Rauta

Kirjoitin

https://github.com/Gerathh/linukka1/blob/main/lshw.png

Tuli listaus laitteista, väylistä, prosessorin tiedoista, kiintolevystä
ja sen osioista, muistin määrästä, näytöstä jne. eli kaikista
laitteista. Sarakkeet ovat H/W path, Device, Class, ja Description eli
(Raudan laiteväylä, Laitem luokka ja kuvaus)

-   HW path on ikään kuin laiteväylän osoite, jonka kautta ko. laite
    löytyy järjestelmästä. Kaikki lähteee root-bus:sta (root-väylä:stä)
    Tämä on hierarkinen myös. Jokaisen laitteen kohdalla voidaan katsoa
    sen kuvausta.

-   Otetaan vaikka rivillä 14 oleva SVGA II Adapter sen H/w path on
    /0/100/2/0/100/ joka on silta 440FX -- 82441FX \[Natoma\] /0/
    VirtualBoxin väylä järjestelmään. (WAU!)

-   lshw siis käyttää hw path:iä näyttääkseen miten laite on liitetty
    käyttöjärjestelmän näkökulmasta

### Aika 2:30

### 

## g)

Käsky

Tämä vaikuttaisi kertovan käyttäjäni sudottamisen eli milloin minä olen
ottanut rootin käyttöön ja kellonajan, milloin sudo päättyy, eli root
oikeudet. Vaikuttaisi olevan noin 10 sekuntia. Kertoo myös terminaalista
jonka laitenimen loppu on 0. Se näyttää missä kansiossa olen ollut.
Tässä tapauksessa /var/log/ ja että olen ottanut siellä rootin, ja
kertoo käskyn minkä olen antanut.

## 

Tämä kertoo mitä tämän koneen kerneli tekee ja milloin. Varoitukset
näyttävät keltaiselta. Virheet punaisella. Täällä tosiaan näkyy kaikki.
Vaikuttaisi että paljon enemmän kuin Windows event viewer.

<https://github.com/Gerathh/linukka1/blob/main/journalctl.png>

### 3:00

## h)

Plugin microniin. Suoritin seuraavat käskyt

https://github.com/Gerathh/linukka1/blob/main/plugin.png

Läheet:

-   <https://en.wikipedia.org/wiki/Command-line_interface> -Tietoa
    CLIstä

-   <https://www.debian.org/doc/manuals/debian-reference/ch02.en.html>
    -Tietoa komentoriviohjelmista

-   <https://manpages.ubuntu.com/manpages/trusty/man8/apt.8.html>
    -Tietoa apt käytöstä

-   <https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited>
    -Perustiedot jota tarvittiin myös tehtävään

-   <https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited>
    -Tehtävänanto

-   <https://www.geeksforgeeks.org/grep-command-in-unixlinux/> -Tietoa
    grepistä

-   <https://www.linux.com/training-tutorials/deep-hardware-discovery-lshw-and-lsusb-linux/#:~:text=This%20abbreviated%20example%20displays%20the%20hardware%20paths%2C%20which,with%20ls%20-l%20%2Fsys%2Fbus%2F%2A%2F%2A%2C%20or%20look%20in%20%2Fproc%2Fbus>.
    -- Opin h/w pathistä

-   <https://micro-editor.github.io/plugins.html> -micron plugarit

Tekijä: Jere Pellinen, Haaga-Helian ammattikorkeakoulu, Tradenomi,
tietojenkäsittely (ei valmistunut vielä)

Helsinki, 2025

