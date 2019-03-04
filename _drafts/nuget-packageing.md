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
Een `.nuspec` bestand is een definitie bestand voor nuget. Dit bestand wordt ingelezen om de library dan op de juiste manier te verpakken naar een package.

~~~
<?xml version="1.0"?>
<package >
  <metadata>
    <id>DevExpress.Core</id>
    <version>1.0.0</version>
    <title>DevExpress Core</title>
    <authors>I**</authors>
    <owners>I**</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>I** licensed DevExpress</description>
    <releaseNotes>First pack</releaseNotes>
    <copyright>Copyright 2019</copyright>
    <tags>I**</tags>
  </metadata>
  <files>
      <file src="bin\DevExpress.Printing.v17.1.Core.dll" target="lib\net45\DevExpress.Printing.v17.1.Core.dll" />
      <file src="bin\DevExpress.Pdf.v17.1.Core.dll" target="lib\net45\DevExpress.Pdf.v17.1.Core.dll" />
      <file src="bin\DevExpress.Utils.v17.1.dll" target="lib\net45\DevExpress.Utils.v17.1.dll" />
  </files>
</package>
~~~

## Auto packaging libraries

De Lib repository wordt met de build server dan automatisch gebuild. De deployment pipline maakt dan een binary, vervolgens wordt er `nuget pack` op aangeroepen met een nuspec file. Zo wordt dan een nupkg file gegenereerd. Die wordt dan gekopieerd naar de lokale package server.

## NuGet.server
NuGet.server is een package die een http(s) nuget repository opzet.
![Initeele pipeline diagram](/assets/installnugetserver.png)
De server accepteerd ook een package die, mits de juiste api key, geupload wordt naar de server.
### Nuget caching proxy server
Om lokaal te kunnen werken wanneer het uplink internet wegvalt kan de package server ook request cachen van de nuget repository. Op die manier zijn alle packages lokaal beschikbaar.
![Initeele pipeline diagram](/assets/nugetlibpipe.png)
