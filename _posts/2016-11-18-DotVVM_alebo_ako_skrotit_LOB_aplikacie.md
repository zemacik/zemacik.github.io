---
layout: blogpost
type: post
title: "DotVVM, alebo ako skrotiť line of business (LOB) aplikácie"
description: "DotVVM, alebo ako skrotiť line of business (LOB) aplikácie"
date: 2016-11-18
categories:
- Framework
tags: [DotVVM, LOB]
published: true
canshare: true
comments: true
---

Pred pár dňami som mal u nás vo firme prednášku o novom webovom frameworku pre ASP.NET - **DotVVM**. Keďže mám tému ešte v hlave bola by škoda ju nespísať na papier a podeliť sa.


## Aké máme dnes možnosti?
---

Z pohľadu .NET vývojára máme dnes v zásade tri cesty akými sa vieme vydať pri vývoji webovej aplikácie 

### 1. ASP.NET WebForms

Môžeme použiť staré ASP.NET WebForms. WebForms nám ponúkali vývoj založený na stránkach a komponentoch. **Na vývoj LOB aplikácií to bolo ako stvorené.** Veľa programátorov koncept nepochopilo, akékoľvek rozvrstvenie aplikácií neexistovalo, a všetka biznis logika bola v samotných stránkach. Aplikácia nebola testovateľná, a po určitom čase bola neudržiavateľná.

Ďalší nešvár WebForms aplikácií bol následne **vygenerovaný HTML kód**, ktorý na dobu s pred 10 rokov možno stačil. Dnes keď potrebujeme aplikáciu cieliť na viac zariadení, obrazoviek, máme responzíviny dizajn táto technológia je takmer nepoužiteľná.

Taktiež spojenie WebForms s javascriptom nebolo moc prívetivé.

A následne **VIEWSTATE**. Kapitola sama o sebe. Nepochopený koncept, kde mali načítané stránky aj niekoľko megabajtov, ktoré následne chodili medzi prehliadačom a serverom.

No a na záver, pre ASP.NET WebForm **nebude podpora v .NET CORE**.

<br/>

### 2. ASP.NET MVC, WEB API, a kopou ďalších JS knižníc

Ďalšou možnosťou je vývoj aplikácie v ASP.NET MVC, WEB API, a kopou ďalších JS knižníc. 
Pri tomto spôsobe vývoja aplikácie, takmer **na všetko potrebujeme vytvárať vlastnú infraštruktúru.**

* či už **validácie** na klientskej, a serverovej strane. A stým spojené udržiavanie rovnakého spôsobu prezentácie výsledkov používateľovi.
* **preposielanie, a formátovanie dátumu a času**, je tiež pekný oriešok
* **lokalizácia** a následné preposlanie na klienta 

Na všetko toto musíme myslieť pri vývoji aplikácie nad ASP.NET MVC

Taktiež potrebujeme veľa, veľa javascriptoveho kódu.

Ak chceme mať aspoň trochu dynamickú stránku, **na všetko potrebujeme javascriptové knižnice**, alebo si funkcionalitu napíšeme sami. Toto všetko udržiavať je celkom výzva.

<br/>

### 3. SPA Framework (Angular, React, Ember, Aurelia), + ASP.NET WEB API

No a tretia možnosť, dnes veľmi moderná, je vývoj SPA (Single page application) v niektorom z tento týždeň populárnych frameworkov, ako sú napríklad Angular JS, React, Vue.js, Aurelia poprípade Ember.js.

Pre mnohé firmy presedlať na tento spôsob vývoja može znamenať vynaloženie značného úsilia, času a finančných prostriedkov do zaškolenia programátorov. Programátori si musia osvojiť veľa nových zručností, konceptov, a technológií.

Ale na rovinu. Nie je to úplne jednoduché sa vo svete javascriptu orientovať.

Ak berieme ohľad aj na udržiavanie existujúceho kódu, .NET platforma je relatívne stabilná, a vieme použiť aj 10 rokov starý projekt, urobiť v ňom zmenu, a opätovne nasadiť. Čo v JS svete môže byť problém, hlavne ak dnes použitý framework, bude zajtra, o týždeň, možno o rok nepodporovaný.

<br/>

 ![DotVVM Logo](/assets/posts/2016/20161118_02_Logo.png){: class="img img-responsive"}

## Na scénu prichádza DotVVM
---

Frustráciu s vývojom webových aplikácií nepociťujem len ja, ale aj ludia z firmy Riganti, konkrétne Tomáš Herceg. On a jeho tím sa rozhodli napísať svoj vlastný framework - DotVVM.

Investovali doň nemálo času. A ako on sám spomínal na jednej svojej prednáške, že keby ohodnotil čas ktorý frameworku vo firme venovali, tak by si mohol kúpiť Teslu. :)

DotVVM je Opensource framework pre ASP.NET.

Ako Tomáš sám o ňom na prednáškach hovorí, píšete v ňom "javascriptové aplikácie bez javascriptu". Ten javascript tam samozrejme je, len s ním tak často neprichádzame do styku, ako je to v skôr popísaných spôsoboch vývoja.

Perfektne sa hodí na vývoj Line of Business (LOB) aplikácií. Hlavne na data entry business aplikácie kde sa rieši kopec formulárov, ich vzťahy a pod. 

Napríklad také aplikácie poisťovní, bánk, ... Vynikajúci príklad je taký formulár na poistenie PZP, zložitejší wizard, kde nasledujúca obrazovka zobrazuje polia podľa hodnôt stránky predzhádzajúcej. 

Nie je úplne vhodný na písanie bežných firemných prezentačných webov (aj keď aj to je možné), aplikácie kde sa veľký dôraz berie na množstvo animácií, a facny funkcionalitu. 

DotVVM je založený na vzore MVVM (Model – View - ViewModel).

- ViewModel je napísaný v C#
- A Views sú V HTML s ďalšími vylepšeniami. 
 
Na klientskej strane DotVVM **používa knižnicu Knockout.js**.

Vývoj v tomto frameworku nám uľahčuje aj rozšírenie do Visual Studia 2015.

Rozprávku o tom ako prebiehal vývoj tohto rozšírenia si môžete pozrieť na videu zo stránky wug.cz. Pozrite sa na to je to celkom zábavné.

<br/>

## Atribúty, Page Livecycle
---

### Binding
Jednotlivé properties vo viewmodeloch môžete odekorovat Binding atribútmi. 
Týmito atribútmi poviete frameworku akým smerom má povoliť bindovanie z a do viewmodelu.

Možnosti ktoré dnes máme sú:

- **None** – Čiže bindovanie je zakázané, a ak príde daná property z klienta bude ignorovaná. Poprípade, an klienta ani nepríde
- **Both** – Default správanie, kde prebieha prenos dať medzi klientom a serverom
- **ClientToServer**, **ServerToClient** sú samo popisné  

### Page Livecycle

Ďalšia vec čo by som chcel spomenúť je životný cyklus stránky. 

 ![Page Livecycle](/assets/posts/2016/20161118_01_PageLiveCycle.png){: class="img img-responsive"}

Ako možete videť na hore uvedenom obrázku, je veľmi podobný tomu z ASP.NET WebForms.

<br/>

## Je DotVVM nové WebForms?
---
Tak ako som už spomínal, DotVVM je do značnej miery inšpirované ASP.NET WebForms, ale moderne, a jednoducho. Rieši problémy ktoré som popísal vyššie.

- **ViewModel je ViewState** 
    - Máme plnú kontrolu nad tým čo a ako tam uložíme.

- **Generovaný výstup**
    - Generovaný výstup komponentov je omnoho elegantnejší, bez akýchkoľvek inline štýlov.
    - Všetko čo natívne komponenty generujú je popísané v dokumentácii na stránke projektu.

- **Testovateľnosť**

Pre WebForm vývojárov je prechod naozaj jednoduchý.

<br/>

## Komponenty
---

Na [stránke projektu](https://www.dotvvm.com/docs/latest) nájdete zoznam základných konponent ktoré framework obsahuje. Iné si môžeme dokúpiť (O tom poviem neskôr), alebo si sami veľmi jednoducho vytvoriť. 

Framework nám ponúka **dve možnosti vytvárania component**.

- Jedna sú takzvané **markup controls**, tie majú koncovku dotcontrol. Je to kus markupu, ktorý môžeme opakovať v rôznych stránkach. Ako napríklad Editor adries. (Adresa dorusenia, Fakturačná adresa) na jednej stránke.

- Potom máme **Code-only controls** tieto nemajú žiadny markup, a všetko sa generuje v kóde. Vieme ich zabaliť do samostatného DLL súboru. Ich vývoj je ale o niečo (možno trošku viac) zložitejší.

<br/>

## Zaujímavé funkcie
---

Ďalej by som chcel spomenúť niekoľko ďalších funkcií ktoré nám framework ponúka.

- Ako som písal vyššie **môžeme si vytvárať vlastné komponenty**.

- Máme tu priamu podporu **ModelValidation**

- Možnosť prepnúť aplikáciu do **SPA režimu** kde sa neprekresľuje pri navigovaní celá stránka, ale prepisuje sa iba content v ContentPlaceholder.

- **ActionFilter** je rovnaký concept ako v MVC

- Priama **integrácia s IoC** (injektovanie závislostí do ViewModelov)

- **Custom presenters** je niečo ako custom HttpHandlers. Použijeme v prípade ak potrebujeme generovať RSS feed, SiteMap a pod.

- **Postback handlers** – pred tým ako sa urobí postback na server vieme vykonať akciu. Napríklad čakať na potvrdenie akcie používateľom, a pod.

<br/>

## Aktuálny stav, Licencia
---

Aktuálne je DotVVM vo verzii 1.0.5

 - RTM je pre plný .NET framework

Ppracujú na podpore pre .NET Core. Niežeby framework nebol funkčný, ale proste len nieje vo verzii RTM. Pevne verím že počas najbližších pár mesiacov bude RTM verzia, keďže dnes tu máme alfa verziu.

Ako som spomínal na začiatku, je to open source framework, a jeho kompletné zdrojové kódy si môžete pozrieť na [githube](https://github.com/riganti/dotvvm). Tak ako Tomáš hovorí, je a vždy bude open source.

Na čom však chcú utŕžiť dáku korunu sú ďalšie komponenty, alebo samotné **rozšírenie do Visual Studia**, ktoré má dve verzie, 

- Free, 
- Professional, ktorá má pokročilejšie funkcie, a aktuálne stojí 129 dolárov.

Podrobné porovnanie si môžeme pozrieť na stránke [DotVVM for Visual Studio 2015](https://www.dotvvm.com/landing/dotvvm-for-visual-studio-extension) 

Ďalšiu z vecí ktoré si už dnes môžeme zakúpiť je [sada komponent]((https://www.dotvvm.com/landing/bootstrap-for-dotvvm)) pre UI framework [Twitter Bootstrap](http://getbootstrap.com/). V tomto prípade sa jedná naozaj o drobné. 

<br/>

## Plány
---

Tak a čo máme plánované do budúcnosti:

- Vydanie verzie pre .NET Core. Ako som už spomínal. 

- Vydanie sady komponent pre business aplikácie s názvom [DotVVM Business Pack](https://www.dotvvm.com/landing/business-pack). Bude obsahovať ďalšie komponenty ktoré nám urýchlia vývoj formulárových aplikácií. Súčasťou budú komponenty ako AutoComplete, ComboBox s podporou šablón, DateTimeRangePicker, ImageUpload, GridView s viac možnosťami. Komponentov má byť až 40. 
Termín uvedenia na trh v tomto momente netuším.

- Ďalšia vec ktorá sa plánuje sú takzvané [Dynamic data](https://github.com/riganti/dotvvm-dynamic-data). Neviem či ste stým reálne v .NETe niekedy pracovali. Ja osobne nie, len si tak matne spomínam že to vedelo vygenerovať komplet formulár na základe jeho modelu a doplnkových atribútov. Len pre úplnosť doplním blog post o [DotVVM Dynamic data](https://www.dotvvm.com/blog/6/Preview-of-DotVVM-Dynamic-Data-Released).

- Potom tu máme veci ako Mimifikácia a bundling JS a CSS súborov.

- Hosting DotVVM aplikácie vo WebView v Xamarin aplikácii, alebo UWP aplikácii. Je to celkom zaujímavé, nechajme sa prekvapiť rýchlosťou takejto aplikácie.

- No a na záver tu máme podporu pre `Electron`. Electron je Framework pomocou ktorého môžeme písať multiplatformové desktopové aplikácie v JS, CSS, a HTML. Nad Electronom je postavené napríklad Visual Sudio Code, GitHub client for Windows, Atom editor, Slack, a mnoho ďalších aplikácií. 


## Zdroje
---

Ešte na záver by som uviedol zopár zdrojov ktoré sa vám možno zídu pri ďalšom štúdiu frameworku.

[Domovská stránka DotVVM](https://www.dotvvm.com/)

[Zdrojové kódy DotVVM, a sample](https://github.com/riganti/dotvvm)

[Sample aplikácia Checkbook](https://github.com/riganti/dotvvm-samples-checkbook)

[Video - DotVVM: "Javascript Apps With No Javascript"](https://channel9.msdn.com/Series/NET-DeveloperDays-2015-on-demand/dotVVM-Javascript-Apps-With-No-Javascript-Tomas-Herceg?ocid=player)

[YouTube séria - Naučte se DotVVM](https://www.youtube.com/watch?v=RrvM46uCouE&list=PLAz0LszWXtZbFRITZR8diXokBP72lkM_g)
