---
layout: post
title: Onderzoek naar huidige buildservers op de markt en bedrijfsinfrastructuur
---

## Inhoud
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

	- [Inhoud](#inhoud)
	- [Huidige infrastructuur](#huidige-infrastructuur)
		- [Source control](#source-control)
		- [Libaries](#libaries)
		- [Huidige build server](#huidige-build-server)
		- [Build configuratie](#build-configuratie)
		- [Gebreken](#gebreken)
	- [Build server](#build-server)
		- [Waarom?](#waarom)
	- [Jenkins](#jenkins)
	- [Azure DevOps](#azure-devops)
	- [Gitlab](#gitlab)
	- [Andere build servers die te duur of irrelevant zijn bevonden](#andere-build-servers-die-te-duur-of-irrelevant-zijn-bevonden)
		- [Travis](#travis)
		- [Buddy](#buddy)
		- [GoCD](#gocd)
		- [Teamcity](#teamcity)
		- [Finalbuilder](#finalbuilder)
- [Demos](#demos)

<!-- /TOC -->
## Huidige infrastructuur
### Source control
![TFS header](/assets/tfsheader.png)

Team foundation server (TFS) 2013 wordt gebruikt als source control. Per klant wordt een repository aangemaakt en in die repository zitten dan projecten.

![File listing](/assets/brfiles.png)


### Libaries
Libraries worden aan de source control toegevoegd in 2 repositories:
- Intern ontwikkelde class libraries (Lib)
- Externe gelicentieerde libraries (LibExt)

Verder wordt er ook gebruik gemaakt van sommige nuget packages. Waardoor een nuget install toch nog nodig is.

Voor SAP of Coresuite aplicaties is er ook nog een current folder. Die folder is gelinkt in de build. Deze folder is initeel leeg wanneer die van de repo wordt gehaald. Het is dan de bedoeling dat de juiste versie van SAP en/of Coresuite naar de current directory worden gekopieerd.

### Huidige build server
![Finalbuild server 7](/assets/finalbuildheader.png)

De huidige build server build projecten wanneer een developer de build triggerd. De successvolle builds worden den gedeployed naar een staging server die ook als ftp server dient.

### Build configuratie
De huidige build configuraties maken gebruike van referencies buiten de huidige repository.
![Build config](/assets/libref.png)

### Gebreken

Wanneer nu een applicatie van de repo gehaald wordt moeten ook de volledige Lib en LibExt opgehaald worden. Dit maakt het builden traag omdat heel wat nutteloze bestanden worden opgehaald. Ook moet de juiste versie van de SAP connector of van Coresuite in de current folder worden gezet. Er moeten dus nog redelijk wat stappen uitgevoerd worden voor een developer klaar is om da huidige repo versie draaiende te krijgen.

Er is momenteel ook nog geen continious integration dus er is dus niet altijd een nieuwste kant en klare versie van de applicatie beschikbaar voor testen.

## Build server
Een build server, ook gekend als een continious integration server, is een systeem die programmas automatisch build in een omgeving die los staat van de ontwikkelaar.

### Waarom?

Een build server is nuttig omdat altijd van een repository vertrokken wordt. Op die manier kan een build een fresh install zijn zonder dat het afhankelijk is van de configuratie van het systeem van de developer. Op deze manier kan getest worden of wel alles om het programma te laten draaien op een repository beschikbaar is.

Een tweede positief punt is continious integration. Na elke commit is een stabiele build beschikbaar.
## Jenkins
![Jenkins header](/assets/jenkinsheader.png)
Jenkins is een CL (Continous Integration) CI (Continous Deployment) server. Deze buildserver is open source, heeft een grote hoeveelheid plugins en een grote support community.

Voordelen:
- Gratis
- Plugins
- Grote community

Nadelen:
- Geen officieele support
- Plugin stability
- Geen job config versioning


## Azure DevOps
![DevOps header](/assets/azuredevopsheaderalt.png)

Voordelen:
- Simpel om te gebruiken

Nadelen:
- Abonnement Visual studio Professional en license voor Windows server nodig
- 6 dollar per gebruiker per maand

## Gitlab
![Gitlab header](/assets/gitlabheader.png)

Voordelen:
- Gratis
- Community

Nadelen:
- Linux

## Andere build servers die te duur of irrelevant zijn bevonden

### Travis
70 dollar per maand
### Buddy
Self hosting aan 175 dollar voor 5 users
### GoCD
Open source maar kleine community
### Teamcity
Free selfhostig 3 agents 100 build configs. Oudere manier van werken.
### Finalbuilder
Standard Edition 359 dollar.
Professional Edition 599 dollar.

# Demos

Gitlab, Jenkins en Azure DevOps worden opgezet om te testen.
