# Modul 300 LB3 Dokumentation

## Inhaltsverzeichnis
- [Einleitung des Projekts](#Einleitung-des-Projekts) 
- [Service Beschreibung](#Service-Beschreibung) 
- [Service Anwendung](#Service-Anwendung) 
- [Grafische �bersicht](#Grafische-�bersicht) 
- [Code Beschreibung](#Code-Beschreibung) 
- [Sicherheit](#Sicherheit) 
- [Testen](#Testen) 
- [Quellenverzeichnis](#Quellenverzeichnis) 

<br>

## Einleitung des Projekts
In der LB3 sollte man eine Umgebung erstellen, welche auf der Docker Container-Technologie basiert. Dabei soll ein Service erstellt werden, welcher innerhalb eines oder mehrer Container implementiert wird. Der Service soll nach dem 'docker-compose up' verf�gbar sein. In dieser LB3 wird ein mySQL Container erstellt, bei dem die Datenbanken per 'localhost:8080' �ber phpMyAdmin verf�gbar sind.

<br>

## Service Beschreibung
  * mySQL Datenbanken �ber phpMyAdmin verf�gbar
  * Die wichtigsten Files, f�r den Dienst: docker-compose.yml, Dockerfile
  * Dienst �ber jeglichen Browser von aussen verf�gbar (Chrome, Firefox, Edge, etc...)
  * Container welche sich in der VM befinden sich in einem privaten Netzwerk und sind  somit nur �ber das eigene Netz erreichbar

<br>

## Service Anwendung
F�r das Starten der VM, auf welchem man das docker-compose.yml und Dockerfile laufen lassen soll, wurde ein passendes Vagrantfile erstellt. Dieses ist im Repository unter M300-Services\LB3\Vagrantfile abgelegt.
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

## Grafische �bersicht
![Grafische �bersicht](Pictures/Grafische_Uebersicht.png)

<br>

