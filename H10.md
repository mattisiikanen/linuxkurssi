# h10_Django


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
Tehtävän tarkoituksena oli tehdä tunnilla käyty harjoitus Django CRM-ohjelmistolla. Aloitin tehtävät 17.2.2023 klo 17:30 käynnistämällä Hyper-V:llä pyörivän palvelimen. Minulta ei löytynyt etukäteen osaamista Pythonista tai Djangosta, joten olin täysin ohjeiden varassa tehtävien osalta. Luin ensiksi läpi opettajamme Tero Karvisen ohjeen Djangon käyttöönotosta nimeltä "Django 4 Instant Customer Database Tutorial".

## a) Kannattavaa. Tee oma tietokantasovellus. jossa on weppiliittymä


### Django asennus

Käytin tehtävään ainoastaan omalla koneella olevaa virtuaalikonetta. Aloitin tehtävän päivittämällä repositoriot komennolla ```sudo apt-get update```, jonka jälkeen siirryin asentamaan Virtualenv paketin ```sudo apt-get -y install virtualenv```</br>
![Kuva1](https://user-images.githubusercontent.com/122887740/219697917-2ff10854-3433-49de-add2-73d1a839d891.png)</br>

Asennus näytti menevän nätisti sisään. Seuraavaksi oli vuorossa luoda uusi virtuaalinen ympäristö, jonka avulla asennettiin viimeisimmät versiot Pythonin paketeista.
Käytin tähän komentoa ```virtualenv --system-site-packages -p python3 env/```, joka näytti myös onnistuvan ongelmitta: </br>
![Kuva2](https://user-images.githubusercontent.com/122887740/219698339-83e4a081-7e83-4a2b-a3b6-24d6653822c3.png) </br>


Kun virtuaaliympäristö oli luotu, oli aika aktivoida se ```source env/bin/activate``` ja aktivoinnin jälkeen tuli tarkistaa, että mihin komennolla ```pip``` viitataan, jottei asennus mene väärään ympäristöön:</br>
![Kuva3](https://user-images.githubusercontent.com/122887740/219699272-fdf00d95-77a8-4ceb-b3e6-a9916cc5e1cb.png)</br>

Tässä tapauksessa minulla oli oikea ympäristö aktivoituna, joten pystyin jatkamaan Djangon asennukseen. Asennusta varten minun tuli kuitenkin ensin luoda määritysiedosto Microlla, jotta ```pip``` osasi asentaa oikean paketin käyttööni:</br>
![Kuva4](https://user-images.githubusercontent.com/122887740/219700090-dd46dfcb-6a1a-470b-8d45-37467e6f5da7.png)</br>


Määritystiedoston jälkeen siirryin lopulta asentamaan Djangon komennolla ```pip install -r requirements.txt```: </br>
![Kuva5](https://user-images.githubusercontent.com/122887740/219700677-207a936f-74fc-4e9c-a4d9-a70d2a5e20d3.png) </br>


Määritystiedosto oli selvästikin määritetty oikein, koska Django asentui koneelle mutkitta. Tein kuitenkin vielä varmistuksena version tarkistuksen Djangoon, jotta viimeisin versio oli asentunut koneelle: </br>
![Kuva6](https://user-images.githubusercontent.com/122887740/219701006-987e45e8-47f7-44a1-adea-8216145ba787.png)


Klo 17:50 lopetin hommat tältä erää tähän, homma jatkuu myöhemmin.

### Djangon konfigurointi
Hommat jatkuivat seuraavana päivänä 18.2.2023 klo 9:54. </br>

Asennuksen jälkeen vuorossa oli konfiguroida Django käyttöön. Aloitinkin luomalla projektin Djangoon komennolla ```django-admin startproject yritysoy``` ja luonnin jälkeen käynnistämällä serverin ```./manage.py runserver```. Käynnistyksen jälkeen navigoin selaimella osoitteeseen ```http://127.0.0.1:8000``` tarkistaakseni palvelimen toiminnan: </br>
![Kuva7](https://user-images.githubusercontent.com/122887740/219849143-43621340-4eb1-4f47-b69c-6ee132684084.png)</br>


Palvelin näytti toimivan oikein!


Testin jälkeen siirryin päivittämään tietokannat komennoilla: ```./manage.py makemigrations``` ja ```./manage.py migrate``` </br>
![Kuva8](https://user-images.githubusercontent.com/122887740/219849345-f97e625a-a859-455b-b6fc-1dab39522f96.png) </br>


Päivitysten jälkeen oli vuorossa luoda käyttäjä ohjelmistoon, mutta ennen luontia tuli asentaa salasanageneraattori, jotta uusille käyttäjille voitiin taata vahva salasana: </br>
![Kuva9](https://user-images.githubusercontent.com/122887740/219849515-9ab83beb-384b-4d55-bb5e-e8498fd98dff.png) </br>


Asennuksen jälkeen loin vahvan salasanan tulevalle käyttäjälle komennolla ```pwgen -s 20 1```, jonka syötin superuserille mattis: </br>

![Kuva10](https://user-images.githubusercontent.com/122887740/219849706-b0be400c-6896-4134-a2cc-7f77b7357627.png) </br>

Käyttäjän luonnin jälkeen oli aika siirtyä testaamaan kirjautumista, mutta palvelimeni oli sammunut migraatioiden ajaksi. Lähdin käynnistämään palvelinta uudelleen, mutta törmäsin seuraavaan ongelmaan: </br>
![Kuva11](https://user-images.githubusercontent.com/122887740/219849873-d78004ba-6489-425f-ac44-ec39e5dd4b76.png) </br>


Jokin toinen palvelu on selvästi kaapannut portin 8000 käyttöönsä, joten päätin Googlata asiaa ja löysin Stack Overflow:sta forumin kyseisestä ongelmasta ja ratkaisun siihen. Oli vuorossa siis tappaa prosessi, joka käyttää porttia 8000 ajamalla komento: ```sudo fuser -k 8000/tcp```. Portin vapautuksen jälkeen käynnistin vielä uudelleen palvelimen ```./manage.py runserver``` ja nyt palvelin lähtikin nätisti jälleen käyntiin. Seuraavaksi navigoin osoitteeseen ```http://127.0.0.1:8000/admin/```: </br>

![Kuva12](https://user-images.githubusercontent.com/122887740/219850082-4e17e9f6-b7ae-43f6-922a-a2f752b48178.png) </br>

Testasin juuri luomiani tunnuksia onnistuneesti. Kirjautumisen jälkeen siirryin luomaan kaksi uutta tunnusta, joille myös määrittelin sopivat oikeudet: </br>
![Kuva13](https://user-images.githubusercontent.com/122887740/219850272-5162123a-2fa2-4102-849d-ce1d957f2a38.png)</br>

Määrittelin tunnuksille seuraavat oikeudet: </br>
- Tilustenvalvoja: Active, Staff status & Superuser status
- Torppari: Active


Määritysten jälkeen päätin kokeilla kirjautumista kummallakin tunnuksella: </br>


![Kuva14](https://user-images.githubusercontent.com/122887740/219850449-63c8d50a-8fed-4bdf-89e8-ed601b154da2.png) </br>
![Kuva15](https://user-images.githubusercontent.com/122887740/219850480-0bdf23d3-c915-4779-8f90-5bc4c53d887c.png) </br>

Oikeudet näyttivät asettuneen oikein tunnusteni kohdalla. Tunnusten luonnin jälkeen siirryin vielä luomaan asiakas tietokannan Djangoon ajamalla komennon ```./manage.py startapp crm```, tämä loi uuden kansion yritysoy-kansion alle nimeltä crm. Seuraavana oli vuorossa konfiguroida asetuksia lisäämällä seuraavaan listaan settings.py tiedoston määritteissä rivi ```'crm',``` käyttäen microa, joka lopulta näytti tältä kokonaisuudessaan: </br>
```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'crm',
]
```
Ja crm/models.py - tiedostoon nämä: </br>

```
from django.db import models

class Customer(models.Model):
   name = models.CharField(max_length=300)
```


Tietojen lisäysten jälkeen oli aika jälleen päivittää tietokannat komennoilla: ```./manage.py makemigrations``` & ```./manage.py migrate```: </br>

![Kuva17](https://user-images.githubusercontent.com/122887740/219851095-8cf6216b-ffc1-47cf-9968-41d2ea6023ce.png) </br>



Päivitysten jälkeen siirryin konfiguroimaan crm kansiossa olevaa admin.py tiedostoa ja lisäsin sinne seuraava tiedot: </br>
```
from django.contrib import admin
from . import models

admin.site.register(models.Customer)
```

Muokkauksien jälkeen käynnistin palvelimen vielä uudelleen komennolla ```./manage.py runserver```, sekä testasin kirjautumista: </br>

![Kuva18](https://user-images.githubusercontent.com/122887740/219851139-6966cb08-69e1-44a6-bd49-c82d9968e408.png)
Customers näkymä oli ilmestynyt näkyviin! Tässä kohtaa pidin pienen tauon ja jatkoin vasta klo 14.11.


Aloitin luomaan uusia asiakkaita Yritys Oy:lle: </br>
![Kuva19](https://user-images.githubusercontent.com/122887740/219865081-1725ffd3-4f0a-42b9-b267-1cde6d8063ed.png)
Olisi kiva saada näkymään asiakkaiden nimet "Customer Object" sijaan. Tämä saatiin korjattua menemällä crm kansioon ja muokkaamalla models.py tiedostoa.

Syötin models.py tiedostoon seuraavat määritteet: </br>
```
from django.db import models

class Customer(models.Model):
    name = models.CharField(max_length=160)

    def __str__(self):
        return self.name
```

Tallensin tiedoston ja navigoin takaisin Djangon hallintaan webselaimessa, sekä päivitin sivun: </br>
![Kuva20](https://user-images.githubusercontent.com/122887740/219865238-f5db890a-b436-4fe8-a7f1-be858f6d9927.png) </br>
Nyt asiakkaani näkyivät oikein!

Otin lopulta vielä vapauden toistaa aiemmat prosessit ja luoda vielä asiakkaiden lisäksi toisen tietokannan nimeltä Products, jonne myös loin esimerkki tuotteita: </br>

![Kuva21](https://user-images.githubusercontent.com/122887740/219865517-29e14f76-53fa-41eb-86c7-5fbe6b20ff11.png)</br>


## Lopetus
Lopetin tehtävien teon klo 14:27. Kyseinen tehtävä jatkoi ja avasi hyvin tietokantoihin ja tietysti pääpainona CRM-ohjelmiston saloihin. Töihin meni tällä erää kokonaisuudessaan n. 2h.

## Lähteet:
Karvinen, Tero, 2022 - Django 4 Instant Customer Database Tutorial (https://terokarvinen.com/2022/django-instant-crm-tutorial/)

Stack Overflow, Django Server Error: port is already in use (https://stackoverflow.com/questions/20239232/django-server-error-port-is-already-in-use)
