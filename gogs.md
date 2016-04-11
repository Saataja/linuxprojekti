#Kokoava ammattiosaamisen näyttö

	Tämä dokumentti on Haaga-Helian Linux projekti –opintojakson kokoava ammattiosaamisen näyttö. Dokumentti luovutetaan ennalta määrättynä ajankohtana opintojakson vastuuopettajalle arvioitavaksi. Opintojaksolla tehtävän projektin aiheena on Go Git Service (Gogs) –palvelun käyttöönotto ja hyödyntäminen. Alempana tässä dokumentissa on yksityiskohtaisempi kuvaus kyseisestä palvelusta.

##Gogs palveluna

	Gogs on Git-versionhallintaohjelmiston sisään rakennettu verkkokäyttöliittymä, joka tarjoaa sen käyttäjälle mahdollisuuden isännöidä haluamaansa palvelua Git-versionhallintaohjelmiston resursseja käyttäen. Gogs-palveluun sisältyy kokoelma itsenäisiä binäärisovelluksia, jotka ovat yhteensopivia tunnetuimpien tietoteknisten käyttöjärjestelmien kuten Windowsin, Linuxin ja Mac OS X:n kanssa. Alla on tarkempi kuvaus toimintaympäristöstä, jossa Gogs otettiin tämän projektin aikana käyttöön. 


###Toimintaympäristö	

	Tässä projektissa Gogs-palvelu asennettiin 64-bittiseen Ubuntu 15.04 –käyttöjärjestelmään. Asennuksen vaiheet on kirjattu alemmas tähän dokumenttiin.  Asennus toteutettiin siten, että ensin etsittiin verkosta Gogs-palvelun asennusohjeet, sen jälkeen niitä testattiin edellä mainitussa käyttöjärjestelmässä ja testauksen jälkeen käyttöjärjestelmä asennettiin uudelleen. Uudelleenasennuksen jälkeen Gogs-palvelun asennus toistettiin ja se sujui ongelmitta. Alempana on tarkempi kuvaus asennuksen vaiheista. 
























####Gogs-palvelun asennus ja käyttöönotto Ubuntu 15.04 –käyttöjärjestelmässä


Gogs-palvelu asennetaan ja otetaan käyttöön avaamalla Pääte-työkalu ja suorittamalla siinä alla olevat komennot niiden ilmoitusjärjestyksessä. Jokaisen komennon jälkeen painetaan Enter-painiketta ja hyväksymällä näin komento suoritettavaksi. Sudo-päätteisten komentojen jälkeen Päätteeseen syötetään järjestelmän pääkäyttäjän salasana.

1. otetaan käyttöön pääkäyttäjän tunnus Päätteessä

sudo su

2. Päivitetään järjestelmän pakettivarastot

apt-get update

3. luodaan järjestelmään uusi seuraavan niminen käyttäjä:

git

käyttäjän salasana on seuraava:

git

adduser git

Syötetään yllä mainittu salasana sille varattuun kenttään ja lopuissa kentissä painetaan Enter-painiketta.

4. annetaan äsken luodulle käyttäjälle pääkäyttäjän oikeudet

visudo

seuraavaavaksi painetaan seuraavaa näppäinyhdistelmää:

CTRL + C

ja kirjoitetaan tiedostoon seuraavat koodirivit:

# User privilege specification
root ALL=(ALL:ALL) ALL
git ALL=(ALL:ALL) ALL

kirjoituksen jälkeen tallennetaan tiedosto painamalla seuraavaa näppäinyhdistelmää:

CTRL + X + Enter


6. Vaihdetaan Päätteen käyttäjäprofiili käyttäjästä root käyttäjään git

sudo su – git

7. asennetaan Git-versionhallintaohjelmisto ja tarkistetaan sen versionumero 

sudo apt-get -y install git

git –version

8. asennetaan MYSQL-tietokanta 

sudo apt-get install mysql-server mysql-server

toimitaan näyttöruudulla näkyvien ohjeiden mukaan

9. tarkistetaan tietokannan tila ja sen versionumero

sudo systemctl status mysql

sudo mysql –version

10. luodaan uusi tietokanta Gogs-palvelua varten seuraavalla komennolla:

sudo mysql -u root -p




























ja kirjoitetaan tiedostoon alla kuvattu sisältö ja klikataan lopuksi Enter-painiketta

mysql> SET GLOBAL storage_engine = 'InnoDB';
Query OK, 0 rows affected, 1 warning (0.00 sec)
		mysql> CREATE DATABASE gogs CHARACTER SET utf8 	COLLATE utf8_bin;
	Query OK, 1 row affected (0.00 sec)
		mysql> CREATE USER 'gogs'@'localhost' IDENTIFIED by 	'gogs123';
	Query OK, 0 rows affected (0.00 sec)
		mysql> GRANT ALL PRIVILEGES ON gogs.* TO 	'gogs'@'localhost' IDENTIFIED BY 'gogs123';
	Query OK, 0 rows affected (0.00 sec)
		mysql> FLUSH PRIVILEGES;
	Query OK, 0 rows affected (0.00 sec)
	mysql> \q

	11. luodaan hakemistoon /home/git seuraavan niminen 	kansio:

	local

	sudo mkdir local
		siirrytään selaamaan kyseistä kansiota ja 	ladataan sinne Gogs-asennuspaketti
		cd local/
			pwd /home/git/local

			sudo
		wget https://storage.googleapis.com/golang/go1.4.2.linux-amd64.tar.gz








			12. puretaan äsken ladattu paketti local-					kansioon

			sudo tar xf go1.4.2.linux-amd64.tar.gz

			13. listataan local-kansion sisältö

			ls

			14. asennetaan go-ohjelmointikieli

			sudo apt-get -y install golang-go

			15. Avataan Go-ohjelmlointikielen käyttöohjeet
			Go





	


