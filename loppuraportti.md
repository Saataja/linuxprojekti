#Projektin loppuraportti

##Johdanto

Tämä dokumentti on Haaga-Helian Linux projekti -opintojaksolla tehtävän projektin loppuraportti. Siinä kuvataan Gogs-työkalun (Go Git Service) asennus ja käyttöönotto vaihe vaiheelta -tyyppisesti Linux Ubuntu 16.04 -käyttöjärjestelmässä.

Gogs (Go Git Service) on Git-versionhallintaohjelmistoon pohjautuva versionhallintapalvelu, joka toimii verkkoselaimessa ja jota sen pääkäyttäjä ylläpitää itsenäisesti. Palvelu eroaa Git-versionhallintaohjelmistosta siinä, että sitä ylläpitävät komponentit on asennettu pääkäyttäjän tietokoneelle ja että sen saatavilla olo ja muu toiminta riippuu täysin pääkäyttäjän toimista. Tämä tarkoittaa, että jos esimerkisi pääkäyttäjän tietokone on sammuksissa, palveluun ei saada yhteyttä. Tällöin pääkäyttäjän tietokone toimii ikään kuin palvelimena Gogs-palvelulle, vaikka siihen ei varsinaisesti olisikaan asennettu palvelinkäyttöjärjestelmää.

Gogs-palvelun pääkäyttäjiä ovat ne käyttäjät, jotka asentavat palvelun tietokoneelleen. Jokaisella heistä on käytössään oma yksityinen Gogs-käyttöympäristö, jota muut käyttäjät voivat alkaa käyttää vain rekisteröitymällä sen käyttäjiksi. Tiettyyn käyttöympäristöön rekisteröityneet käyttäjät voivat luoda yhteisiä tietovarastoja sekä käyttöympäristön sisällä toimivia vuorovaikutuksellisia organisaatioita. Kyseiset organisaatiot ovat samantyyppisiä kuin Windows Server -palvelinkäyttöjärjestelmissä esiintyvät organisaatioyksiköt. 

Tietovarastojen ja organisaatioiden luomisen lisäksi käyttäjät voivat kopioida mahdollisissa muissa julkaisualustoissa olevat tietonsa Gogs-palveluun. Tämä tarkoittaa sitä, että jos sama käyttäjä käyttää Gogs-palvelun lisäksi esimerkiksi Github-palvelua, hän voi kopioida tai siirtää tietonsa Github:sta Gogs:iin ja päinvastoin. Kyseistä tietojen siirto- tai kopioimisprosessia kutsutaan migraatioksi.

##Gogs-palvelun asennuksen ja käyttöönoton valmistelu

Ennen Gogs-palvelun asentamista ja käyttöönottoa asennetaan Linux Ubuntu 16.04 -käyttöjärjestelmä 
ja tehdään asennuksen yhteydessä siihen käyttäjä nimeltään git.

Asennuksen jälkeen avataan järjestelmän Unity-valikon kautta työkalu nimeltään Pääte. Se tapahtuu klikkaamalla järjestelmän oikeassa reunassa näkyvän pystypalkin ylintä kuvaketta ja kirjoittamalla avautuvaan hakukenttään seuraava termi: Pääte. Tämän jälkeen kirjoitetaan avautuvaan ikkunaan alla listatut komennot järjestyksessään yksi kerrallaan. Jokaisen komennon kirjoittamisen jälkeen suoritetaan se painamalla Enter-painiketta. Jos järjestelmä kysyy lupaa jollekin toimenpiteelle, annetaan lupa painamalla K-kirjainta.

##Gogs-palvelun asennus Päätteen avulla

Alla on lista komennoista, joiden avulla Gogs saadaan toimimaan. Ne tulee syöttää
Päätteeseen järjestyksessään yksi kerrallaan ja jokaisen komennon jälkeen tulee
painaa Enter-painiketta.

1. sudo apt-get -y update && sudo apt-get -y upgrade

#(Huomio! Tässä vaiheessa järjestelmä kysyy Ubuntu 16.04 -käyttöjärjestelmänasennuksen yhteydessä määriteltyä pääkäyttäjän salasanaa. Ennen kuin komento voidaan suorittaa, se täytyy syöttää sille varattuun kenttään ja painaa sen jälkeen lopuksi Enter-painiketta. Yllä mainitun komennon avullapäivitetään Ubuntun pakettivarastot ja asennetaan järjestelmään saatavilla olevat päivitykset)

Komennon tulisi antaa seuraavanlainen tuloste:

Tehdään asetuksia: xinit (1.3.4-3ubuntu0.1) ...

Tehdään asetuksia: oxideqt-codecs:amd64 (1.14.7-0ubuntu1) ...

Tehdään asetuksia: liboxideqtcore0:amd64 (1.14.7-0ubuntu1) ...

Tehdään asetuksia: liboxideqtquick0:amd64 (1.14.7-0ubuntu1) ...

Tehdään asetuksia: liboxideqt-qmlplugin:amd64 (1.14.7-0ubuntu1) ...

Processing triggers for libc-bin (2.23-0ubuntu3) …




seuraavaksi asennetaan git-versionhallintaohjelmiston sisältävät paketit seuraavalla komennolla:

sudo apt-get -y install git




komennon tulisi antaa seuraavanlainen tuloste:

Processing triggers for man-db (2.7.5-1) ...

Tehdään asetuksia: liberror-perl (0.17-1.2) ...

Tehdään asetuksia: git-man (1:2.7.4-0ubuntu1) ...

Tehdään asetuksia: git (1:2.7.4-0ubuntu1) …



seuraavaksi tarkistetaan Git-ohjelmistopaketin versio seuraavalla komennolla:

git --version

komennon tulisi antaa seuraavanlainen tuloste:

git version 2.7.4



seuraavaksi ladataan Gogs-palvelun asennuspaketti alla olevan linkin takaa.
Ladattu tiedosto tallentuu hakemistoon nimeltään Lataukset, josta se siirretään hakemistoon nimeltään Koti.

https://dl.gogs.io/gogs_v0.9.13_linux_amd64.tar.gz



Seuraavaksi klikataan pakettia kotihakemistossa hiiren kakkospainikkeella ja avataan se sovelluksella Pakettienkäsittely. Sen jälkeen klikataan sovelluksessa Pura-painiketta, siirrytään seuraavassa ikkunassa kotihakemistoon ja klikataan lopuksi näyttöruudun oikeassa alakulmassa näkyvää Pura-painiketta. Kun kotikansiossa on oranssi alikansio nimeltään Gogs, purkaminen on onnistunut.



Seuraavaksi siirrytään takaisin Päätteeseen ja asennetaan siinä mysql-tietokantapalvelin seuraavalla komennolla:

sudo apt-get -y install mysql-server

asennuksen yhteydessä järjestelmä pyytää määrittämään uuden salasanan tietokannan pääkäyttäjälle nimeltään root. Määritellään sille asennusikkunassa kahdesti seuraava salasana: data

Kun Pääte antaa seuraavanlaisen tulosteen:





Tehdään asetuksia: libhtml-template-perl (2.95-2) ...

Tehdään asetuksia: mysql-server (5.7.12-0ubuntu1) ...

Processing triggers for libc-bin (2.23-0ubuntu3) ...

Processing triggers for ureadahead (0.100.0-19) ...

Processing triggers for systemd (229-4ubuntu4) …




tietokanta on onnistuneesti asennettu.
		
7. seuraavaksi tarkistetaan mysql-tietokannan versio seuraavalla komennolla:

 mysql --version
 
 
 
 
 		
 komennon tulisi antaa seuraavanlainen tuloste:

mysql  Ver 14.14 Distrib 5.7.12, for Linux (x86_64) using  EditLine wrapper



seuraavaksi tarkistetaan tietokannan tila seuraavalla komennolla:

sudo systemctl status mysql

komennon tulisi antaa seuraavanlainen tuloste:




KUVA PUUTTUU



seuraavaksi siirrytään seuraavaan hakemistoon:
		/home/git/gogs 
		
Se tapahtuu seuraavalla komennolla:
cd /home/git/gogs

komennon tulisi antaa seuraavanlainen tuloste:



 git@git-Lenovo-B50-45:~/gogs$ 

10. seuraavaksi käynnistetään Gogs-palvelu seuraavalla komennolla:

./gogs web

komennon tulisi antaa seuraavanlainen tuloste:



KUVA PUUTTUU



Tässä vaiheessa jätetään Pääte auki taustalle ja siirrytään käyttämään Firefox-selainta. 
Seuraavilla sivuilla on tarkemmat ohjeet jatkotoimenpiteistä.



seuraavaksi avataan Firefox-selain ja siirrytään sillä seuraavaan osoitteeseen: 

http://localhost:3000/install
tämän jälkeen selainikkunassa tulisi näkyä seuraavanlainen näkymä:

KUVA PUUTTUU





kun yllä kuvattu Gogs-palvelun asennusikkuna on saatu avattua Firefox-selaimessa,
jätetään se taustalle ja avataan uusi Pääte-ikkuna Ubuntun Unity-valikon kautta.
Tässä vaiheessa näyttöruudulla tulisi olla seuraavanlainen näkymä:



seuraavaksi varmistetaan, että Gogs-palvelu on edelleen käynnissä ensimmäisessä Pääte-ikkunassa 
ja sen jälkeen siirrytään äsken avatussa tyhjässä Pääte-ikkunassa 
seuraavaan hakemistoon: 

/home/git/gogs
Se tapahtuu seuraavalla komennolla:





cd /home/git/gogs



seuraavaksi annetaan kaikille käyttäjille suoritusoikeudet seuraavaan tiedostoon:





scripts/mysql.sql

Se tapahtuu seuraavalla komennolla:





sudo chmod +x scripts/mysql.sql






yllä mainittujen komentojen syöttämisen jälkeen Päätteessä tulisi olla seuraavanlainen näkymä:

KUVA PUUTTUU



seuraavaksi luodaan tietokanta aiemmin asennetulle tietokantapalvelimelle.

Se tapahtuu seuraavalla komennolla:

mysql --user=root --password=data < scripts/mysql.sql







komennon tulisi antaa seuraavanlainen tuloste:

mysql: [Warning] Using a password on the command line interface can be insecure.









Yllä olevasta varoituksesta ei tarvitse välittää. 
Mikäli muita varoituksia ei komennonsyöttämisen jälkeen tullut, tietokannan luonti onnistui.



Seuraavaksi siirrytään takaisin Firefox-selaimessa olevaan Gogs-palvelun asennusikkunaan 
ja kirjoitetaan siinä näkyvään Password-laatikkoon seuraava salasana:

data


Lopuksi siirrytään hiirellä asennusikkunan alareunaan ja klikataan siellä olevaaInstall Gogs -painiketta.



###Gogs-palvelun käyttöönotto

Asennuksen jälkeen palveluun pitää rekisteröityä. 
Se tapahtuu klikkaamalla Login-ikkunassa seuraavaa linkkiä: Sign up now.




Tämän jälkeen syötetään omat tiedot seuraavassa ikkunassa oleviin laatikoihin alla olevan kuvan mukaisesti ja klikataan lopuksi Create an account -painiketta. Lopuksi äsken luoduilla tunnuksilla kirjaudutaan palveluun seuraavassa ikkunassa. Kirjautumisen jälkeen näyttöruudulla tulisi olla kuvan 3 mukainen näkymä.

###Sisällön luominen Gogs-palveluun

Gogs-palvelun käyttöliittymässä on mahdollista luoda seuraavia sisältökomponentteja:






1. tietovarastot (repositories) → Gogs:in sisälle rakennettavia tietovarastoja voidaan verrata Linux-käyttöjärjestelmän hakemistoihin. Jokaiseen yksittäiseen asiaan liittyvä tieto on koottu yhteen tietovarastoon samalla tavoin kuin Linuxissa kaikki käyttäjän henkilökohtaiset tiedostot on koottu sen kotihakemistoon. 




2. tietojen kopioiminen tai siirtäminen toisesta julkaisualustasta Gogs-palveluun (Migration) → toisesta julkaisualustasta on mahdollista siirtää tai kopioida tietoja Gogs:iin. Jos sama käyttäjä käyttää esimerkiksi sekä Github- että Gogs-palveluita, Github:in tiedot voidaan kopioida Gogs:iin Migraatio-toiminnon avulla.





3. organisaatiot → organisaatiot ovat Gogs:in sisälle luotavia hallinnollisia toimielimiä, joille voidaan luoda omia tietovarastoja. Niitä voidaan verrata Windows Server -palvelinkäyttöjärjestelmässä esiintyviin organisaatioyksiköihin. Organisaatiot 		voidaan luokitella ja nimetä niiden tehtävän tai hallinnollisen aseman mukaan ja niihin on mahdollista lisätä ja poistaa jäseniä. Myös organisaatioiden oikeuksia voidaan muuttaa niiden tehtävän ja hallinnollisen aseman mukaan. 





###Tietovaraston luominen

Tietovaraston luominen tapahtuu klikkaamalla Dashboard-näkymässä näyttöruudun oikeassa yläkulmassa olevaa +-merkkiä ja valitsemalla New repository.




Luodaan tietovarasto nimeltään Esimerkkivarasto ja säädetään sen asetukset alla olevan mallikuvan mukaisiksi. Language-laatikon arvoksi kannattaa aina asettaa Go ja License-laatikon arvoksi GNU General Public License v3.0. Lopuksi klikataan Create repository -painiketta.




Koska esimerkkivarastoa tullaan käyttämään pohjana myöhemmin luotaville varastoille, sen kohdalla rastitetaan seuraava valintaikkuna: Initialize this repository



Tietovaraston luomisen jälkeen näyttöruudulla tulisi näkyä kuvan 3 mukainennäkymä. Siitä voidaan päätellä, että kyseiseen tietovarastoon on varastoitu kaikki siihen liittyvä tieto.





