---
layout: post
title: Git vs Team foundation server
---

Er zijn tegenwoordig heel wat version control systemen beschikbaar op de markt. Het is dus misschien goed om even een korte uiteenzetting te geven van de verschillende soorten version control.

# Soorten version control

## Local data

Dit is de oudste versie van version control. Hier gaat het over version management met developers op hetzelfde filesysteem.

### Voorbeelden

- Revision Control System (RCS) houd versies bij per file en slaat de deltas op.

## Client server

Hier gaat het over version management met een gedeelde server als repository. Veranderingen kunnen dan naar de server geupload worden. Hier worden de verschillende versies dan op de server bijgehouden.

### Voorbeelden
- Team foundation server: Microsoft oplossing voor een client-server version control.
- Subversion: Open source client-server oplossing van Apache.

## Distributed

Distributed systemen werken zoals een client-server systeem maar dan met een extra stap. De repository wordt lokaal bij de devoloper helemaal opgeslaan. Veranderingen worden in de lokale repository opgeslaan. De extra stap is dan dat de lokale repository dan wordt gesyncroniseerd met de server.

### Voorbeelden
- Git: Git is een open source wereld bekende oplossing voor version control.

## Afwegingen
Als er tegenwoordig aan softwaredevelopment wordt gedaan wordt local data version control quasie nooit gebruikt. Developers gebruikten typtisch machines met verschillende bestand systemen. Client-server version control wordt tegenwoordig wel nog gebruikt. Maar de meest voorkomende version managament is de distributed variant. Deze heeft het voordeel over client-server dat het de developer offline laat ontwikkelen met toegang tot alle versies van de code. Het is dan ook makkelijker om te zien welke veranderingen lokaal zijn gemaakt tegenover de repository.

Het nadeeel van dit systeem is dat de repository van de developer ni altijd gesyncroniseerd is met de server. Af en toe moet de repository geupdate worden zodat de veranderingen van de server naar de lokale repository kunnen worden geupdate en vice versa.

# Welk systeem is het beste

Welke systeem is nu het beste om te gebruiken? Dat hangt af van de situatie.
## Nog geen version management
Wanneer er nog geen version management bestaat is de beste oplossing om te gaan voor een distributed systeem zoals Git. Deze oplossing is het meest flexibel en breed ondersteund door zowel bedrijven als een grote community. Er zijn heel wat oplossingen om Git in de cloud te krijgen, maar er zijn ook veel self-managed oplossingen.

### Self hosting
Self hosting brengt heel wat nadelen met zich mee zoals: server kosten, configruatie en updates. Maar het brengt ook wat voordelen met zich mee. Zo kan je zoveel data hosten als je zelf wilt zowel privé als publiek. Je bent dus volledig baas van je eigen code.

Voor self hosting is er een groot aanbod. Er zijn ook heel wat build servers die git bevatten als deel van de oplossing. Deze zijn ook interessant voor Continous Integration.
#### [Git](https://git-scm.com/)
![Githeader](/assets/githeader.png)
Als er enkel en repository nodig is zonder meer dat is dit de beste oplossing. Er is geen web interface aan gelinkt. De interactie met Git gebeurd dus volledig met ssh.

`git remote add origin ssh://git@server/repo->path.git`

Waar path het pad voor de git user is op de server.
#### [Gitea](https://gitea.io/)
![Gitea header](/assets/gitea.png)
Gitea is een Git oplossing met een webinterface. Deze is lightweight en gratis om te self hosten. Er is issue tracking release tagging. Kortom alles wat nodig is voor een simpele git server.
#### [GitLab](https://about.gitlab.com/)
![GitLab](/assets/gitlabproject.png)
Gitlab is een DevOps tool met git integratie. Hierin zit alles wat verwacht wordt van een Git webserver en meer. CI en CD is beschikbaar per project. Elke repository is hier dan een project met een pipline. De pipeline wordt dan ingesteld door ofwel AutoDevops ofwel een bash script. AutoDevops zoekt de juiste build tool voor het builden van het programma en stuurt het door naar een agent met minimale nood voor configuratie. GitLab is alleen beschikaar voor Linux als native applicatie.
#### [Azure DevOps](https://azure.microsoft.com/en-us/services/devops/)
![Azure](/assets/azuredevopsheader.png)
Azure DevOps volgt dezelfde structuur als GitLab. Elke repository is ook een project met een pipline etc... Het grote verschil zit hem in dat azure ook TFS ondersteuning bied. En daarinboven kan het ook geinstalleer worden op een windows server als native applicatie.

### Cloud oplossing
Wanneer er geen infrastructuur bestaat voor zelf server te hosten is een cloud oplossing te overwegen.
#### Azure DevOps
Azure Devops is gratis voor teams met minder dan 5 mensen. Vanaf 10 mensen begint het aan $30 per maand. Verder zijn de build minuuten ook beperkt afhankelijk van het betaalplan.
### Gitlab
GitLab is gratis voor zoveel gebruikers als je wilt met 2000 pipline minuuten online en self hosted runners. Er zijn ook nog extra betalende features beschikbaar.
### GitHub
![Azure](/assets/azuredevopsheader.png)
GitHub teams kost 9$ per maand per user. Github bied ook enkel een git oplossing.
## Wanneer migereren

Wanneer een niet distributed content management systeem gebruikt wordt kan getwijfeld worden om over te gaan naar een distributed systeem. Wanneer het huidige systeem stabiel werkt wordt beter niet gemigreerd. Enkel wanneer er plannen zijn om te veranderen van infrastructuur is het de tijd en moeite waard.


# Besluit
Een version management systeem is nodig om in teams te programmeren. De betere systemen zijn distributed en de bekendste is Git. Gebruik Git tenzij er al een version management systeem draait die goed werkt en minstens client-server is.
