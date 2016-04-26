Projektin loppuraportti

	Tämä dokumentti on Haaga-Helian Linux projekti -opintojaksolla tehtävän projektin loppuraportti. Projektissa asennetaan ja otetaan käyttöön Gogs (Go Git Service) -palvelu sekä sen liitännäiskomponentit Ubuntu 15.04 -käyttöjärjestelmässä. Tähän dokumenttiin on kirjattu kaikki projektin aikana tehdyt toimenpiteet vaihe vaiheelta -tyyppisesti sekä havainnollistettu ja selitetty niiden lopputulokset. Dokumentin avulla kenen tahansa on tarkoitus pystyä toteuttamaan sama projekti uudelleen ja mahdollisesti jopa kehittää sitä tulevaisuudessa. 

Gogs on Go-ohjelmointikielellä toteutettu työkalu, jonka avulla käyttäjä voi helposti luoda itse ylläpitämiään palveluita, jotka pohjautuvat Git-versionhallintaohjelmistoon. Kyseinen työkalu on yhteensopiva suosituimpien käyttöjärjestelmien kuten Windowsin, Linuxin ja Mac OS X:n kanssa. 













































Projektin vaiheet


			Alle on kirjattu selitykset projektin aikana tehdyistä toimenpiteistä 			eli sen vaiheista.

			1. avataan pääte kirjoittamalla Unity-valikon hakupalkkiin seuraava 			termi: 

		pääte

	ja painamalla lopuksi Enter-painiketta

	2. annetaan käyttäjälle pääkäyttäjän oikeudet kirjoittamalla 	päätteeseen seuraava komento:

	sudo su

	ja kirjoitetaan pääkäyttäjän salasana sille varattuun kohtaan













	
	
		3. kirjoitetaan päätteeseen seuraavat komennot yksitellen painaen 	jokaisen komennon jälkeen Enter-painiketta

	sudo apt-get update 
	(päivittää Ubuntun pakettivarastot)

	adduser git
	(luo uuden käyttäjän nimeltään git)

	määritellään uudelle käyttäjälle salasana kahdesti ja sen jälkeen 	painetaan Enter-painiketta kunnes pääte kysyy, ovatko kaikki tiedot 	oikein. Tämän jälkeen painetaan lopuksi K-kirjainta.


























		kirjoitetaan päätteeseen seuraava komento:

	sudo visudo

	ja etsitään tiedostosta seuraava rivi:

	# User privilege specification
	root ALL=(ALL:ALL) ALL

	tämän jälkeen lisätään sen alle seuraava rivi:

	git ALL=(ALL:ALL) ALL

	lopuksi tallennetaan muutokset painamalla seuraavaa 	näppäinyhdistelmää: CTRL + X + K + Enter

	(antaa git-käyttäjälle pääkäyttäjän oikeudet)

	kirjaudutaan ulos järjestelmän nykyiseltä käyttäjältä klikkaamalla 	järjestelmän oikeassa yläkulmassa näkyvää ratasta ja valitsemalla 	kirjaudu ulos. Sen jälkeen kirjaudutaan uudelleen sisään git-	käyttäjänä ja avataan pääte sillä.

	sudo apt-get -y install git
	(asentaa git-paketin)

	git --version
	(näyttää git-paketin version)

	sudo apt-get  -y install mysql-server
	(asentaa mysql-palvelimen)

	päätteen kysyessä mysql-tietokannan pääkäyttäjän salasanaa, 	seuraava salasana määritellään sille varattuun kenttään kahdesti:

	data




















			sudo systemctl status mysql -l
			(näyttää mysql-palvelimen tilan)

			sudo mysql --version
			(näyttää mysql-tietokannan version)


			sudo mysql -u root -p
			(avaa tietokannan muokkaustilan pääkäyttäjän oikeuksilla
			HUOM! Kysyy äsken määriteltyä pääkäyttäjän salasanaa 			ennen avautumistaan)

			kirjoitetaan tietokantaan seuraava rivikokonaisuus:


			SET GLOBAL storage_engine = 'InnoDB';
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















Gogs-palvelun asennus ja käyttöönotto

	Alle on listattu Gogs-palvelun asennuksen ja käyttöönoton vaiheet 	sekä siihen tarvittavat komennot.

	sudo apt-get -y install golang-go
	(asentaa Go-kielen järjestelmään)

	ladataan Gogs-palvelun asennuspaketti alla näkyvän linkin takaa ja 	siirretään se latauksen valmistuttua käyttäjän kotikansioon

	https://dl.gogs.io/gogs_v0.9.13_linux_amd64.tar.gz

	puretaan paketti kotikansioon Ubuntun pakettienkäsittelyohjelmalla

	kirjoitetaan päätteeseen seuraavat komennot:

	cd /home/git/gogs

	./gogs web

	tämän jälkeen päätteessä pitäisi olla alla olevan kuvan mukainen 	näkymä.


Lopuksi poistutaan näkymästä painamalla seuraavaa näppäinyhdistelmää:
CTRL + C




		




		
	
	Seuraavaksi asennetaan Supervisor-työkalu ja otetaan se käyttöön. Sillä valvotaan Gogs-palvelua ja sen asennus tapahtuu kirjoittamalla päätteeseen seuraavat komennot:

	sudo apt-get -y install supervisor
	(asentaa supervisor-paketin)

	sudo mkdir -p /var/log/gogs
	(luo tallennuspaikan Gogs-palvelun lokitiedostoille)

	sudo nano /etc/supervisor/supervisord.conf
	(avaa supervisor-työkalun asetusmäärittelytiedoston pääkäyttäjän 	oikeuksilla)

	muokataan tiedostoa painamalla ensin seuraavaa 	näppäinyhdistelmää: CTRL + O + Enter ja sen jälkeen 	kirjoittamalla tiedoston loppupäähän seuraava 	tekstirivikokonaisuus:

		[program:gogs]
	directory=/home/git/go/src/github.com/gogits/gogs/
	command=/home/git/go/src/github.com/gogits/gogs/ web
	autostart=true
	autorestart=true
	startsecs=10
	stdout_logfile=/var/log/gogs/stdout.log
	stdout_logfile_maxbytes=1MB
	stdout_logfilebackups=10
	stdout_capture_maxbytes=1MB
	stderr_logfile=/var/log/gogs/stderr.log
	stderr_logfile_maxbytes=1MB
	stderr_logfile_backups=10
	stderr_capture_maxbytes=1MB
	environment = HOME="/home/git", USER="git"

	lopuksi tallennetaan muutokset painamalla seuraavaa 	näppäinyhdistelmää: CTRL + X + K + Enter

	alla on kuva tiedostosta muutosten jälkeen.

















			sudo service supervisor restart
			(käynnistää supervisor-työkalun uudelleen)

			sudo systemctl status supervisor -l
			(näyttää supervisor-työkalun tilan)

			mikäli päätteeseen ilmestyy yllä olevan komennon syöttämisen 			jälkeen allaolevan kuvan mukainen näkymä, kaikki toimii 				supervisor-työkalun osalta tarkoituksen mukaisesti.

		











































	
			Seuraavaksi asennetaan nginx-palvelin ja tehdään siitä käänteinen 			välityspalvelin. Se tapahtuu kirjoittamalla päätteeseen seuraavat 			komennot:

			sudo apt-get -y install nginx
			(asentaa nginx-paketin)

			ifconfig
			(tarkistetaan käytettävän työaseman ip-osoite ja 				kirjataan se ylös. Osoite on kirjattu seuraavaan 				kohtaan: wlan0 inet addr:)

			sudo nano /etc/nginx/sites-available/gogs
			(avaa nginx-palvelimen tunnistamien verkko-osoitteiden listan 			pääkäyttäjän oikeuksilla)

			muokataan tiedostoa painamalla ensin seuraavaa 				näppäinyhdistelmää:

			CTRL + O + Enter ja sen jälkeen kirjoittamalla tiedostoon seuraava 			tekstirivikokonaisuus:

			server {
		listen 80;
		server_name työaseman ip-osoite (esim. 192.168.10.62;

		proxy_set_header X-Real-IP  $remote_addr; # pass on real client IP
		location / {
		proxy_pass http://localhost:3000;
			}
			}

			lopuksi tallennetaan muutokset painamalla seuraavaa 				näppäinyhdistelmää:

			CTRL+ X + K + Enter








		sudo ln -s /etc/nginx/sites-available/gogs /etc/nginx/sites-enabled/gogs
		(asettaa äsken määritellyn ip-osoitteen gogs-palvelun käyttöön)

		sudo service nginx restart
		(käynnistää nginx-palvelimen uudellen)

		sudo systemctl status nginx -l
		(näyttää nginx-palvelimen tilan)

		Tämän jälkeen päätteeseen pitäisi ilmestyä alla olevan kuvan mukainen näkymä. 		Jos näin tapahtuu, kaikki toimii myös nginx-palvelimen osalta tarkoituksen 		mukaisesti.










				Koko asennus- ja käyttöönottoprosessin lopuksi kirjoitetaan internet-selaimen 		osoiteriville seuraava termi: localhost 

		ja painetaan Enter-painiketta. Jos selaimeen ilmestyy alla olevan kuvan 			mukainen näkymä, asennus on onnistunut ja kaikki toimii tarkoituksen mukaisesti.