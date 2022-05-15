# Modul 300 LB3 Dokumentation

## Inhaltsverzeichnis
- [Einleitung des Projekts](#Einleitung-des-Projekts) 
- [Service Beschreibung](#Service-Beschreibung) 
- [Service Anwendung](#Service-Anwendung) 
- [Grafische Übersicht](#Grafische-Übersicht) 
- [Code Beschreibung](#Code-Beschreibung) 
- [Sicherheit](#Sicherheit) 
- [Testen](#Testen) 
- [Quellenverzeichnis](#Quellenverzeichnis) 

<br>

## Einleitung des Projekts
In der LB3 sollte man eine Umgebung erstellen, welche auf der Docker Container-Technologie basiert. Dabei soll ein Service erstellt werden, welcher innerhalb eines oder mehrer Container implementiert wird. Der Service soll nach dem 'docker-compose up' verfügbar sein. In dieser LB3 wird ein mySQL Container erstellt, bei dem die Datenbanken per 'localhost:8080' über phpMyAdmin verfügbar sind.

<br>

## Service Beschreibung
  * mySQL Datenbanken über phpMyAdmin verfügbar
  * Die wichtigsten Files, für den Dienst: docker-compose.yml, Dockerfile
  * Dienst über jeglichen Browser von aussen verfügbar (Chrome, Firefox, Edge, etc...)
  * Container welche sich in der VM befinden sich in einem privaten Netzwerk und sind  somit nur über das eigene Netz erreichbar

<br>

## Service Anwendung
Für das Starten der VM, auf welchem man das docker-compose.yml und Dockerfile laufen lassen soll, wurde ein passendes Vagrantfile erstellt. Dieses ist im Repository unter M300-Services\LB3\Vagrantfile abgelegt.
Um die VM zu starten, kann man folgenden Befehl eingeben:

    cd '[Pfad_von_Vagrantfile]'
    vagrant up

Danach muss man diese Ordnerstruktur erstellen: <br>
_______________________________________
| <br>
| <br>
| - docker-compose.yml <br>
| - Dockerfile <br>
| <br>
| <br>
_______________________________________

Danach muss man den jeweiligen Code in die Files hineinkopieren. Danach in der Befehlszeile folgenden Befehl eingeben:

    docker-compose up
    oder
    docker-compose -d

Im Browser folgendes eingeben, um auf den Dienst zu kommen:

    http://localhost:8080
    Benutzer: root
    Passwort: mysql-password

<br>

## Grafische Übersicht
![Grafische Übersicht](Pictures/Grafische_Uebersicht.png)

<br>

## Code Beschreibung
 Vollständige und dokumentierte Code des docker-compose.yml File:

    #Version festlegen
    version: '1.0'

    #Beginn der Services
    services:
    #Ersten Container festlegen
    db:
    #Image fuer den ersten Container festlegen
        image: mysql:8.0
    #Containernamen festlegen
        container_name: mysql
    #Festlegen, dass der Container immer neustarten soll, sobald dieser gestoppt wurde
        restart: always
    #Das root-Passwort fuer die Datenbank wird festgelegt
        environment:
            MYSQL_ROOT_PASSWORD: mysql-password

    #Zweiten Container festlegen    
    app:
    #Legt die Abhaengigkeit zum ersten Container fest
        depends_on:
        - db
    #Image fuer den ersten Container festlegen
        image: phpmyadmin/phpmyadmin
    #Containernamen festlegen
        container_name: phpmyadmin
    #Festlegen, dass der Container immer neustarten soll, sobald dieser gestoppt wurde
        restart: always
    #Der Port 80 wird auf den port 8080 umgeleitet
        ports:
        - '8080:80'
    #Legt den mySQL Host fest
        environment:
            PMA_HOST: db
    #Erstellt ein Image mit dem dazugehoerigen Dockerfile
        build: .

Zusätzlich noch der Code des dazugehörigen Dockerfile:

    #Ist dafuer zustaendig, dass das docker-compose.yml File ein Image, namens ubuntu erstellen kann
    FROM ubuntu
    #Hört den Port 80 ab
    EXPOSE 80

<br>

## Sicherheit
* Der Benutzer ist 'root' und das Passwort ist 'mysql-password'
* Container die sich auf der VM befinden, sind in einem ptivaten Netzwerk und sind somit nur über das eigene Netz erreichbar

<br>

## Testen
* Testen kann man den Dienst über Browser
* Wenn der Service über die Adresse http://localhost:8080 erreichbar ist, ist der Test erfolgreich
* Getestet wurde der Dienst mit Edge, Firefox und Chrome
* Test war erfolgreich über Edge, Firefox und Chrome
* Im Terminal den Befehl 'docker ps' eingeben, um zu schauen, ob die Container am laufen sind
* Falls Vagrant File nicht gefunden wird, eventuell Verzeichnis im Verzeichnis "\LB3" den Ordner "Vagrant" erstellen und dort das Vagrantfile reinkopieren

<br>

## Quellenverzeichnis

| Beschreibung      | Quelle          |
| --------------| -----------------|
| Docker-Compose Vorlage für Code | https://hub.docker.com/r/phpmyadmin/phpmyadmin |
| Dockerhub |  https://hub.docker.com/ |