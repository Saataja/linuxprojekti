#Projektin loppuraportti

Tämä dokumentti on Haaga-Helian Linux projekti -opintojaksolla tehtävän projektin loppuraportti. Siinä kuvataan Gogs-palvelun (Go Git Service) asennus ja käyttöönotto vaihe vaiheelta -tyyppisesti Linux Ubuntu 16.04 -käyttöjärjestelmässä.

Gogs (Go Git Service) on työkalu Git-versionhallintaohjelmistoon pohjautuvien palveluiden itsenäiseen ylläpitoon. Työkalu on tehty Go-ohjelmointikielellä ja se voidaan asentaa ja ottaa käyttöön kaikissa tunnetummissa käyttöjärjestelmissä kuten Windowsissa, Linuxissa ja MAC OS X:ssä.

##Gogs-palvelun asennuksen ja käyttöönoton valmistelu

Ennen Gogs-palvelun asentamista ja käyttöönottoa asennetaan Linux Ubuntu 16.04 -käyttöjärjestelmä ja tehdään asennuksen yhteydessä siihen käyttäjä nimeltään git.

Asennuksen jälkeen avataan järjestelmän Unity-valikon kautta työkalu nimeltään Pääte. Se tapahtuu klikkaamalla järjestelmän oikeassa reunassa näkyvän pystypalkin ylintä kuvaketta ja kirjoittamalla avautuvaan hakukenttään seuraava termi: Pääte. Tämän jälkeen kirjoitetaan avautuvaan ikkunaan alla listatut komennot yksi kerrallaan. Jokaisen komennon kirjoittamisen jälkeen suoritetaan se painamalla Enter-painiketta. Jos järjestelmä kysyy lupaa jollekin toimenpiteelle, annetaan lupa painamalla K-kirjainta.

sudo apt-get update

sudo apt-get -y install git

sudo apt-get -y install mysql-server

#TROLOLOL







