# h7 Maalisuora
## a)

     Kirjoita hello world kolmella kielellä.
 ### javascript:
      Webbisivulla JS:llä sen voi toeuttaa bupottamalla se html sisään eli avaa tekstieditorin laittaa tuon siihen ja tallentaa vaikk hello.html ja avaa selaimessa:

```
<!DOCTYPE html>
<html>
<head>
  <title>Hello World</title>
</head>
<body>
  <h1>Check the console!</h1>
  <script>
    console.log("Hello, World!");
  </script>
</body>
</html>

```

Paina f12 ja sieltä consoli niin hello world näkyy.


### Python

Avaa tekstieditori.
kirjoita   print("Hello, World!") ja tallenna se vaikka nimellä hello_world.py

Python tulee olla asennettuna

![Python](https://github.com/Gerathh/linukka1/blob/main/h71.jpg)


### C++

Käytän Microsoft visuel studio 2022.

```
      #include <iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;  // Print "Hello, World!"
    return 0;
}

```
![C++](https://github.com/Gerathh/linukka1/blob/main/h72.jpg)


Painan ctrl + shift + B to build it

---
## b)

Tein tiedoston moikka jonka tallensin /usr/local/bin/moikka

 ---

`sudo nano /usr/local/bin/moikka`


Sen jälkeen annoin tarvittavat oikeudet

`sudo chmod +x /usr/local/bin/moikka`

![](https://github.com/Gerathh/linukka1/blob/main/h73.jpg)

## d)

   Osaisin varmaankin muttten ymmärrä tehtävänantoa @@

---


## e)


* Latasin uusimman VirtualBoxin

![VirtualBox](https://github.com/Gerathh/linukka1/blob/main/h74.jpg)


* Latasin uusiman Debian version osoitteesta https://www.debian.org/download
* Virtualboxissa luon uuden koneen machine-->New
* Annoin nimeksi Debian12, ja Mounttasin juuri lataamani asennusmedian kohtaan ISO Image

![vbox asetukset](https://github.com/Gerathh/linukka1/blob/main/h75.jpg)

* Painan Next jossa vaihdan käyttäjänimekseni jere ja salasanaksi 12345 ja toistan sen vielä. Olen aiemmin ladannyt Guest additionin joten painoin täpän siihen sitten painan jälleen Next

![Asetuksia](https://github.com/Gerathh/linukka1/blob/main/h76.jpg)


*Annan muistia 8192 MB ja ytimiä 8, sittenpainan jällen next

![muistijaytimet](https://github.com/Gerathh/linukka1/blob/main/h77.jpg)

*seuraavalla sivulla jätän kakki oletuksille ja painan Next

![oletukset](https://github.com/Gerathh/linukka1/blob/main/h78.jpg)

*Seuraavalla sivulla näen yhteenvedon asetuksista. Painan sitten Finnish.

![yhteeenveto](https://github.com/Gerathh/linukka1/blob/main/h79.jpg)

 *Nyt käyttöjärjestelmä asentaa itseään tovin.

 ![](https://github.com/Gerathh/linukka1/blob/main/h710.jpg)

`![](https://github.com/Gerathh/linukka1/blob/main/h711.jpg)`

---
##Jaan virtuaalikoneen googledriven kautta. Minun piti palauttaa tämä klo 12 kun luulin että viiden jälkeen. Mutta tässä tämä nyt on kuitenkin.

*  https://drive.google.com/drive/folders/1FJHpRhcUuSYIDM_84NxhtJB6fpzhChJQ?usp=sharing

---



## Lähteet:
https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

https://terokarvinen.com/2007/12/04/shell-scripting-4/

https://www.youtube.com/watch?v=876aSEUA_8c - javascriptin opettelua ja kertausta

https://www.codecademy.com/learn - koodausharjoituksia

https://www.w3schools.com/  - koodausharjoituksia