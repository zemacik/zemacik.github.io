---
layout: blogpost
type: post
title: "Novinky z konferencie Microsoft Build 2016 (SK)"
description: "Novinky z konferencie Microsoft Build 2016"
date: 2016-04-02
categories:
- Konferencie
tags: [Konferencie, Poznámky]
published: true
canshare: true
comments: true
---

#### Termín: 30.03.2016 - 01.04.2016

#### Videá: [Channel 9](https://channel9.msdn.com/Events/Build/2016)

V tomto príspevku by som chcel zhrňúť moje zápisky z konferencie Build 2016, ktorá skončila len asi pred 12timi hodinami.

--- 

## Deň 1
### Keynote

**Visual Studio**

- Visual Studio 2015 Update 2
- nové Visual Studio 15 Preview
    - veľmi svižne, zrýchlenie niektorých komponent, a úkonov až o 1000 %
    - rýchla inštalácia (cca do 5 min.)

**Vývoj**

- nový Typescript 1.8
    - bohatá kontextová nápoveda vo VS Code, a veľkom VS 2015
    - mám pocit že Typescript 1.8 je už viac tool ako jazyk

**Ostatné**

- Bash vo windows (Linux userspace pre windows)
    - 2 hlavné komponenty
        - Genuine Ubuntu user-mode binaries provided by Canonical
        - Window Subsystém for Linux (WSL)
            - priamo od MS
    - [Link](https://msdn.microsoft.com/commandline/wsl/about)

- Desktop App Converter - Win32 aplikácie do Windows Store
    - sandboxovane aplikácie
- zjednodušený vývoj pre Xbox One - Xbox Dev Mode - premení konzolu na vývojársky nástroj
    - prepínanie konzoly medzi dvomi režimami
- HoloLens
    - [Galaxy explorer sample source code](https://github.com/Microsoft/GalaxyExplorer)
- [Congitive services](https://www.microsoft.com/cognitive-services/)- Coratana, API, ML
    - [Pricing](https://www.microsoft.com/cognitive-services/en-us/pricing) 
- [Microsoft Bot framework](https://dev.botframework.com/) - Preview
    - Conversation as a platform
    - Conversation is the new UI
    - [BotBuilder](https://github.com/Microsoft/BotBuilder)
    - Vytvoríme WEB API
- [Azure Functions](https://azure.microsoft.com/en-us/services/functions/)

---

## Den 2
### Keynote

**Xamarin**

- free pre profesional a Enterprise verziu Visual Studia 2015
- pre Community Edition to bude podľa môjho názoru obmedzené (bolo to povedané tak zahmlene)
    - takže nie, James Montemagno tweetol že tam nie je žiadne obmedzenie

- IOs emulátor aj pre Windows, ale na buildovanie stále treba mať Mac.
    - prenáša obrazovku na windows z Macu

**Power BI**

- PowerBI embedded
     - umožňuje vložiť komponentu power BI na stránku

**MS Office**

- JS addins v MS Office 365
- generovanie js addinov cez yeoman
- DocuSign for Office - podpisovanie dokumentov
- MS Office Online je free
- Uvoľnená nová verzia Office Tools pro Visual Studio

**SQL**

- [Microsoft SQL Server Developer Edition is now free](https://blogs.technet.microsoft.com/dataplatforminsider/2016/03/31/microsoft-sql-server-developer-edition-is-now-free/?wt.mc_id=WW_CE_DM_OO_SCL_TW&Ocid=C+E%20Social%20FY16_Social_TW_SQLServer_20160331_414281610)

**Ostatne**

- *Azure DocumentDB* má [zmenenú cenovú politiku ](https://azure.microsoft.com/en-us/pricing/details/documentdb/) odvíjajúcu sa podľa rýchlosti, a množstva dát ktoré sú kladené na DB
- Azure DocumentDB podporuje klientov MongoDB (čiže MongoDB protokol). Wow !
- Azure DocumentDB už podporuje geo replikáciu
- Azure Service Fabric je v produkcii

---

## Den 3
### Keynote

nebola


---

## Prednášky

- Prednaska: **[Visual Studio 2015 Extensibility](https://channel9.msdn.com/Events/Build/2016/B886)**
    - Od: Mads Kristensen
    - Extensibility Tool 2015 - súbor nástrojov, šablón na to aby sme mohli písať vlastne rozšírenia pre VS 2015
        - treba mať nainštalované Visual Studio SDK
        - New project VSIX Project
        - AppVeyor - CI server - služba, ktorá zostaví build rozšírenia a poskytne ho na stiahnutie
            - AppVeyor.com - free
            - vsixgalllery.com - staging prostredie pre nightly buildy rozšírení od Mads Kristensena
            - ak je rozšírenie otestované, manuálne ho uploadneme  do VS Extension Gallery (stiahmene ho z AppVeyor)
    - Zdrojové kódy rozšírenia ktoré naprogramovaná počas prednášky - [FileDiffer](https://github.com/madskristensen/FileDiffer)

---
- Prednaska: **[ASP.NET Core Deep Dive into MVC](https://channel9.msdn.com/Events/Build/2016/B812)**
    - Od: Scott Hunter, Daniel Roth
    - viac menej prednáška bola opakovaním už predchádzajúcich prednášok z iných konferencií, a predstavení ASP.NET Core
    - Novinka: dnx vrstva je preč, miesto toho sa používajú .NET Core tools
    - ASP.NET core features
        - Hosting
            - kestrel, self hosting
        - Middleware
            - Routing, Logging, Static files, diagnostics, error hangling, sessions, CORS, localization, custom...
        - DI
        - Configuration
        - Logging
        - Application frameworks
            - MVC, identity, SignalR
    - ASP.NET  Core -> Unified stack -  Webpages, MVC, Web API
    - _ViewImports.cshtml 
        - importovanie namespaces do views
        - importovanie tag helperov
    - TagHelpers
        - podľa moho názoru čistý bordel :-/
        - vôbec neriešia hlavný problém, s vytváraním znovu použiteľných komponetov
        - čím viac na ne pozerám, tým viac viem že ich nechcem používať, a s najväčšou pravdepodobnosťou začnem písať UI konečne ako SPA (či už s použitím Aurelia aleo Angular frameworku), a .NET Core bude iba ako API vrstva + bootstrap webu.

---
- Prednáška: **[HoloLens: Building UWP 2D Apps for Microsoft HoloLens](https://channel9.msdn.com/Events/Build/2016/B854)**
    - Od: Dave Lindsay
    - ak je aplikácia Touch friendly je aj hololens/gesture friendly (UWP App)
    - existujúce nástroje pre UWP aplikácie funguje aj pre aplikácie pre HoloLens
    - Je k dispozícii emulátor [http://dev.windows.com/holographic](http://dev.windows.com/holographic)

---

## Odkazy na dema / zdrojové kódy

[MyDriving](https://azure.microsoft.com/en-us/campaigns/mydriving/) - IoT, Azure, ML, Xamarin,  .... a kopec ďalších technológií - ! Super demo ! [source](https://github.com/Azure-Samples/MyDriving)

[HoloLens Galaxy explorer](https://github.com/Microsoft/GalaxyExplorer)

[FileDiffer Visual Studio 2015 Extension ](https://github.com/madskristensen/FileDiffer)
