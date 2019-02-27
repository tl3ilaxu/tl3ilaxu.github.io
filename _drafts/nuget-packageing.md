---
layout: post
title: Package management
---
Tegenwoordig kan je niet meer goed programmeren zonder gebruik te maken van een package manager. Voor .net toepassingen wordt tegenwoordig NuGet gebruikt.

Mometeel wordt er in het bedrijf gebruik gemaakt van externe libraries via NuGet. De interne libraries worden aan een source control meegegeven. Dit zorgt voor problemen als projecten moeten gesandboxed worden. De oplossing is dus om de interne libraries ook aan de package manager toe te voegen.

In het ideaal geval voegen we de packages toe aan onze repository, en wordt er een Nuget install opgeroepen die alle interen en externe libraries installeerd.

# Nuget
Nuget is een package manager ontwikkeld door microsoft. Deze is standaard geinstalleerd in Visual Studio sinds 2012.

## Nuget pack

C# class libraries kunnen door nuget verpakt worden naar nu `.nupkg` files. Dit kan in Visual studio gebeuren via de NuGet console of via de interface.

NuGet is er ook in client vorm.
![Initeele pipeline diagram](/assets/nugetcommand.png)

Via `nuget pack` kan dan automatisch een package worden gemaakt.

## Nuget spec

## Auto packaging libraries


De Lib repository wordt met de build server dan automatisch gebuild. De deployment pipline maakt dan een binary, vervolgens wordt er `nuget pack` op aangeroepen met een nuspec file. Zo wordt dan een nupkg file gegenereerd. Die wordt dan gekopieerd naar de lokale package server.
