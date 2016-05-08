#Projektin loppuraportti

Tämä dokumentti on Haaga-Helian Linux projekti -opintojaksolla tehtävän projektin loppuraportti. Siinä kuvataan Gogs-työkalun (Go Git Service) asennus ja käyttöönotto vaihe vaiheelta -tyyppisesti Linux Ubuntu 16.04 -käyttöjärjestelmässä.

Gogs (Go Git Service) on Git-versionhallintaohjelmistoon pohjautuva versionhallintapalvelu, joka toimii verkkoselaimessa ja jota sen pääkäyttäjä ylläpitää itsenäisesti. Palvelu eroaa Git-versionhallintaohjelmistosta siinä, että sitä ylläpitävät komponentit on asennettu pääkäyttäjän tietokoneelle ja että sen saatavilla olo ja muu toiminta riippuu täysin pääkäyttäjän toimista. Tämä tarkoittaa, että jos esimerkisi pääkäyttäjän tietokone on sammuksissa, palveluun ei saada yhteyttä. Tällöin pääkäyttäjän tietokone toimii ikään kuin palvelimena Gogs-palvelulle, vaikka siihen ei varsinaisesti olisikaan asennettu palvelinkäyttöjärjestelmää.

Gogs-palvelun pääkäyttäjiä ovat ne käyttäjät, jotka asentavat palvelun tietokoneelleen. Jokaisella heistä on käytössään oma yksityinen Gogs-käyttöympäristö, jota muut käyttäjät voivat alkaa käyttää vain rekisteröitymällä sen käyttäjiksi. Tiettyyn käyttöympäristöön rekisteröityneet käyttäjät voivat luoda yhteisiä tietovarastoja sekä käyttöympäristön sisällä toimivia vuorovaikutuksellisia organisaatioita. Lisäksi he voivat kopioida tietoa muista julkaisualustoista käyttämäänsä käyttöympäristöön. Edellä mainitut vuorovaikutukselliset organisaatiot ovat samantyyppisiä kuin Windows Server -palvelinkäyttöjärjestelmässä esiintyvät organisaatoyksiköt.






##Gogs-palvelun asennuksen ja käyttöönoton valmistelu

Ennen Gogs-palvelun asentamista ja käyttöönottoa asennetaan Linux Ubuntu 16.04 -käyttöjärjestelmä ja tehdään asennuksen yhteydessä siihen käyttäjä nimeltään git.

Asennuksen jälkeen avataan järjestelmän Unity-valikon kautta työkalu nimeltään Pääte. Se tapahtuu klikkaamalla järjestelmän oikeassa reunassa näkyvän pystypalkin ylintä kuvaketta ja kirjoittamalla avautuvaan hakukenttään seuraava termi: Pääte. Tämän jälkeen kirjoitetaan avautuvaan ikkunaan alla listatut komennot järjestyksessään yksi kerrallaan. Jokaisen komennon kirjoittamisen jälkeen suoritetaan se painamalla Enter-painiketta. Jos järjestelmä kysyy lupaa jollekin toimenpiteelle, annetaan lupa painamalla K-kirjainta.

###Gogs-palvelun asennus Päätteen avulla

Alla on lista komennoista, joiden avulla Gogs saadaan toimimaan. Ne tulee syöttää Päätteeseen **yksi kerrallaan** ja jokaisen komennon jälkeen tulee painaa **Enter**-painiketta.

1. sudo apt-get update  
(päivittää Ubuntun pakettivaratot)

2. sudo apt-get -y install git  
(asentaa git-versionhallintaohjelmiston sisältävän paketin, johon gogs pohjautuu)

3. 

