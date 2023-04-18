# H8SayMyName
Tehtävää 8 varten.

## Lukuläksy
Tällä erää ei ollut lukuläksyä.


## Ympäristö

Hyper-V kotikoneella (Host):

- CPU: i5-9600K
- RAM: 16Gb
- HDD: 120Gb
- Win 11 Pro x64

Virtuaalikoneen speksit:

- 2 x CPU
- 4 Gb RAM
- 50 Gb HDD
- Generation 2 (Hyper-V pyytää määrittelemään)

## Aloitus 
Tehtävän tarkoituksena oli ostaa / vuokrata omalla nimellä domain joltain suositulta nimipalveluntoimittajalta.
Aloitin tehtävät 11.2.2023 klo 10:26.


## a) Vuokraa domainnimi ja aseta se osoittamaan virtuaalipalvelimeesi
Aloitin valitsemalla palveluntarjoajaksi Namecheapin ja menemällä heidän sivuille tarkistamaan hakukoneesta, onko domain ```mattisiikanen``` vapaana.</br>
![Kuva1](https://user-images.githubusercontent.com/122887740/218248399-061dd81c-378f-4d8f-8f32-d4a3e07d62e0.png)</br>


Domain oli käytettävissä, joten vuokrasin sen vuodeksi. Namecheap yritti pakkomyydä kaikkia lisäpalveluja, mutta jätin ne valitsematta ja siirryin suoraan kassalle.
Kassalla sai vielä päättää, otetaanko käyttöön sekä Auto-Renew että Domain Privacy. Kävin kävin lukemassa Domain Privacysta Namecheapin tarjoamasta linkistä. Domain Privacy suojaa domainin rekisteröijän tiedot, jottei tiedot omistajuudesta vuoda julkisuuteen, tämä suojaa rekisteröijää monelta harmilta. </br>


![Kuva2](https://user-images.githubusercontent.com/122887740/218248670-c7379530-a997-4b38-bca9-12f522f0959e.png) </br>

Seuraavalla sivulla oli näkyvissä alla olevat tiedot, jotka esitän tietosuojasyistä vain otsikoina:
- Registrant Contact
- Administrative Contact
- Technical Contact
- Billing Contact


Lopuksi oli luvassa ostoksen teko ja tilauksen viimeistely. Kun ostokset oli tehty, tuli osoittaa oma domain vuokrattuun virtuaalipalvelimeen.
Jotta pääsin alkuun, tuli minun ensin kirjautua Linoden isännöintipalveluun ja käydä kaappaamassa omistamani palvelimen julkinen IP-osoite tulevaa DNS muutosta varten.


![Kuva3](https://user-images.githubusercontent.com/122887740/218252520-fd0d0eb0-5150-422b-83ca-16cfb8097a9f.png) </br>

IP-osoitteen jälkeen palasin Namecheapin hallintaan, josta valitsin Account -> Domain list -> mattisiikanen.com -> Manage -> Advanced DNS.


Hallinnassa lisäsin 2 kpl A tietueita seuraavilla tiedoilla: </br>
@-ohjaus:


- Host: @              
- Value: 143.42.18.59   
- TTL: 5 min           


www-ohjaus:


- Host: www
- Value: 143.42.18.59
- TTL: 5 min



![Kuva4](https://user-images.githubusercontent.com/122887740/218253195-4722ce6a-947a-463b-9886-9c5b837614ac.png)


Julkaisun jälkeen odottelin 5 minuuttia, jotta DNS tietueet päivittyvät ympäri maailman.

Koitin ensin käyttää ```curl``` komentoa: </br>
![Kuva5](https://user-images.githubusercontent.com/122887740/218253241-4d13ec9f-a6f5-4deb-9e3c-24f9d6ece780.png)


Ja seuraavaksi koitin jo selata Firefoxilla sivuille: </br>

![Kuva6](https://user-images.githubusercontent.com/122887740/218253249-ef4295e4-8e05-4905-82b9-34983f4feed8.png)


Ohjauksien jälkeen liikenne näytti ohjautuvan oikein Linodessa isännöityyn palvelimeen.


## b) Tutki oman nimesi tietoja 'host' ja 'dig' -komennoilla. Analysoi tulokset.
Klo 10:45


DNS hankinnan ja konfiguroinnin jälkeen luvassa oli tutkia oman domainin komennoilla ```host``` ja ```dig```.

Aloitin komennolla ```host mattisiikanen.com```: </br>
![Kuva7](https://user-images.githubusercontent.com/122887740/218253589-b21bc148-4691-4159-b93a-c8be9749275b.png)</br>


Tietojen perusteella domainilla ```mattisiikanen.com``` on yksi IP-osoite: 143.42.18.59, eli DNS-hallintaan syöttämäni tietue, sekä 5 eri palvelinta spostin ohjausta varten.


Seuraavana luvassa oli komento ```dig mattisiikanen.com```: </br>
![Kuva8](https://user-images.githubusercontent.com/122887740/218253695-a46bd5d1-b253-48dc-8451-1d7ab1585f7c.png)</br>

Jotta ymmärsin jotain tiedoista, tuli minun ensin perehtyä ```dig``` komennon saloihin selailemalla Linuxizen artikkelia Dig Command in Linux (DNS Lookup) aiheesta.

Tiedoista selviää seuraavaa: </br>
- <<>> DiG 9.16.37-Debian <<>> mattisiikanen.com <- näyttää käytetyn työkalun version tiedot + haetun domainin
- Got answer <- sisältää teknisen tiedon pyynnöstä 
- OPT PSEUDOSECTION <- kertoo DNS-tietueessa käytetyistä laajennuksista
- QUESTION SECTION <- kysely, jolla kerätään tietueet DNS:stä
- ANSWER SECTION <- Vastaus kyselylle, jossa näytetään löydetyt tietueet
- Query time & etc <- tässä on statistiikkaa varten löytyvää tietoa

```Host``` komento selvästi keskittyy domainin päätason asioihin, kuten IP-osoitteeseen ja palvelinosoituksiin. ```Dig``` taas tuntuu enemmän pureutuvan domainin teknisiin tietoihin ja itse siihen määritettyihin tietueisiin.


## Lopetus
Lopetin tehtävien teon klo 11:57. Kyseinen tehtävä avasi hyvin domainin vuokrausta ja DNS-tietueiden julkaisua. Töihin meni tällä erää n. 1,5h.

## Lähteet:
Namecheap, What is domain privacy? (https://www.namecheap.com/security/what-is-domain-privacy-definition/)


Linuxize, 26.2.2020 - Dig Command in Linux (DNS Lookup) (https://linuxize.com/post/how-to-use-dig-command-to-query-dns-in-linux/)
