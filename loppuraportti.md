#Projektin loppuraportti - Johdanto

Tämä dokumentti on Haaga-Helian Linux projekti -opintojaksolla tehtävän projektin loppuraportti. Siinä kuvataan Gogs-työkalun (Go Git Service) asennus ja käyttöönotto vaihe vaiheelta -tyyppisesti Linux Ubuntu 16.04 -käyttöjärjestelmässä.

Gogs (Go Git Service) on Git-versionhallintaohjelmistoon pohjautuva versionhallintapalvelu, joka toimii verkkoselaimessa ja jota sen pääkäyttäjä ylläpitää itsenäisesti. Palvelu eroaa Git-versionhallintaohjelmistosta siinä, että sitä ylläpitävät komponentit on asennettu pääkäyttäjän tietokoneelle ja että sen saatavilla olo ja muu toiminta riippuu täysin pääkäyttäjän toimista. Tämä tarkoittaa, että jos esimerkisi pääkäyttäjän tietokone on sammuksissa, palveluun ei saada yhteyttä. Tällöin pääkäyttäjän tietokone toimii ikään kuin palvelimena Gogs-palvelulle, vaikka siihen ei varsinaisesti olisikaan asennettu palvelinkäyttöjärjestelmää.

Gogs-palvelun pääkäyttäjiä ovat ne käyttäjät, jotka asentavat palvelun tietokoneelleen. Jokaisella heistä on käytössään oma yksityinen Gogs-käyttöympäristö, jota muut käyttäjät voivat alkaa käyttää vain rekisteröitymällä sen käyttäjiksi. Tiettyyn käyttöympäristöön rekisteröityneet käyttäjät voivat luoda yhteisiä tietovarastoja sekä käyttöympäristön sisällä toimivia vuorovaikutuksellisia organisaatioita. Kyseiset organisaatiot ovat samantyyppisiä kuin Windows Server -palvelinkäyttöjärjestelmissä esiintyvät organisaatioyksiköt. 

Tietovarastojen ja organisaatioiden luomisen lisäksi käyttäjät voivat kopioida mahdollisissa muissa julkaisualustoissa olevat tietonsa Gogs-palveluun. Tämä tarkoittaa sitä, että jos sama käyttäjä käyttää Gogs-palvelun lisäksi esimerkiksi Github-palvelua, hän voi kopioida tai siirtää tietonsa Github:sta Gogs:iin ja päinvastoin. Kyseistä tietojen siirto- tai kopioimisprosessia kutsutaan migraatioksi.

## Gogs-palvelun asennus Pätteen avulla





