---
layout: post
title: Design van een demo pipeline
---
De huidige workflow zoals besproken in deze [post]({% post_url 2019-02-16-buildserver-vergelijkingen %}) is niet ideaal. Toch moet er een build server demo gemaakt worden die werkt met de huidige workflow.


# Design pipeline

## Focus
Minimale workflow verandering.
Futurproofing.


## Eerst pipeline
![Initeele pipeline diagram](/assets/initialpipelinediagram.png)

En snelle manier om een pipeline op te zetten, zonder dat er moet gekeken worden naar de interne libraries, is om de hele root van de TFS server te downloaden.

Deze aanpak werkt en er kan makkelijk een demoproject gebuild worden. Een klein nadeel van deze pipeline is dat er 40Gb aan data moet binnengehaald worden om 1 enkel project te builden.

## Revisie

Piplines zijn ontworpen om met 1 source repository te werken. Wat logisch is want builds moeten ook gesandboxed kunnen worden om getest en gedeployed te worde.

Dit is een probleem om met de huidige workflow te werken. Hier heeft elke pipeline 3 repositories nodig. De source repository en dan de 2 library repositories.

![Revisited pipeline diagram](/assets/revisitedpipeline.png)

Deze pipeline gebruikt een pipeline trigger om ander piplines aan te roepen midden in het process.

Deze pipeline gaat al heel wat sneller. Nu worden alleen nog maar alle interne en extern gelicencieerde libraries gedownload. Dit zijn wel nog steeds de libraries voor alle projecten.

Verder is er ook nog een race conditie die zich voordoet wanneer de project repository minder lang moet downloaden dan het project zelf. Dit doet zich voor wanneer de libraries voor het eerst gedownload moeten worden. De libraries zijn ongeveer 5 Gb en het project dat gebuild wordt is typisch niet zo groot.

## Pipeline 3
![Revisited 2 pipeline diagram](/assets/revisitedpipeline2.png)

Deze pipeline lost de race conditie op en voegt parallelisatie toe voor de library downloads.

## Pipeline 4
![Revisited final pipeline diagram](/assets/revisitedpipeline3.png)

Deze pipeline optimalizeerd de snelheid voor deze workflow.

# Library versioning

Zoals vermeld in de vorige post wordt gebruik gemaakt van een "current" folder om zo de huidig te builden libraries te managen. In die folder wordt dan een kopie gemaakt van de libray zijn juiste versie.

Om dit werkende te krijgen voor een demo maken we gebruik van een symlink.

![Library pipeline diagram](/assets/libraryPipe.png)


De symlink wordt dan gelockt vanaf de build begint tot nadat `nuget restore` gebeurd is.
Er wordt ook een file aan de repo toegevoegd die de versie bevat van de library. In dit geval `SAP.version`.

~~~
9.3.0.7
~~~
