---
layout: blogpost
type: post
title: "Vytvárame vlastné rozšírenie pre Visual Studio Code (SK)"
description: "Vytvárame vlastné rozšírenie pre Visual Studio Code"
date: 2016-02-22
categories:
- Visual Studio
tags: [VS Code, tutorial]
published: true
canshare: true
comments: true
---

Nedávno som vypublikoval svoje prvé rozšírenie pre Visual Studio Code (VS Code). Dnes by som chcel v pár 
riadkoch zhrnúť s čím som sa musel popasovať. Ako som spomínal v [minulom príspevku][100], na písanie blogov
používam Visual Studio Code, a keď píšem, aby som pravdu povedal, nepoužívam diakritiku. Som na to 
tak zvyknutý, a tak mi to vyhovuje. Proste píšem rýchlejšie. Následne použijem dáky nástroj ktorý 
mi diakritiku pridá automaticky.

Donedávna som používal [stránku brm.sk/diakritika][1]. Ale ešte som si chcel prácu uľahčiť, tak som sa rozhodol,
spojiť príjemné s užitočným a vytvoriť rozšírenie do editora Visual Studio Code. 

**A vôbec som nečakal že to bude také jednoduché**

## Čo budeme potrebovať?

Keďže samotné VS Code je naprogramované v javascripte, nad jadrom Elektrón, aj rozšírenia pre tento editor sa 
neprogramujú v ničom inom.

#### Node.js
Ako prvú vec budeme potrebovať mať nainštalovaný `node.js`. Dnes už ho určite máte nainštalovaný, ale keby nie tak
si ho môžete stiahnuť zo stránky [nodejs.org][2] pre Windows, a tak isto pre iné platformy. 
Node.js budeme potrebovať na nainštalovanie yeomana, balíčkov ktoré budeme pri vývoji potrebovať a tak isto na 
publikovanie samotného rozšírenia do VS Code Marketplace.

#### Yeoman
Ak máme node.js nainštalované, môžeme pristúpiť k inštalácii `Yeomana`. [Yeoman][3] je generátor šablón, projektov,
a pod. Ak používať veľké visual studio tak by som ho prirovnal ku generátoru projektov ak dáte `File -> New Project`.
Yeoman nainštalujeme pomocou príkazu 

`npm install -g yo`

#### generator-code
Ďalšia vec ktorú budeme potrebovať sú samotné šablóny pre projekt rozšírenia do VS Code. Tie nainštalujeme tiež pomocou 
node.js do gobálneho úložiska balíčkov, tak isto ako yeomana, keďže je predpoklad že budeme yeomana, aj šablóny používať pri 
viacerých projektoch.

`npm install -g generator-code`
  
#### vsce
[VSCE][4] je balíček, ktorý tam s procesuje celú mágiu s vytvorením balíčka z naho projektu, ktorý potom môžeme nahrať 
priamo na server s rozšíreniami, alebo nám naše balíčky aj sám vypublikuje. 

`npm install -g vsce`


## Generujeme nový projekt pre rozšírenie

Tak, ak už máme všetky prerekvizity nainštalované, môže prejsť ku vytváraniu samotného rozšírenia. 
Na vytvorenie samotného rozšírenia som postupoval podľa návodu na [stránke VS Code][5].

1. Otvoríte si príkazovú riadku (konzolu) 
    `cmd`

2. Presuniete sa do priečinka kde chcete vygenerovať šablónu pre vaše rozšírenie 
    `cd c:\dev\text`

3. Vygenerujeme si mustru nášho projektu. Tento príkaz nám spustí yeoman generátor.
    `yo code`

4. Ďalej di môžeme vybrať aký typ rozšírenia chceme vygenerovať. Ja osobne som použil rozšírenie programované v [Typescripte][6].

![Running Yo code command](/assets/posts/2016/20160222_01_running_yo_code.png){: class="img img-responsive"}

5. Vyplníme údaje ktoré po nás generátor požaduje. Publisher Name môžete získame na stránke [Publish Extensions][7]. 
Linka je schovaná dolu na strake s [rozšíreniami][8] pre VS Code. Ak niektoré údaje teraz zlé vyplníte, nič sa nebojte. 
V projektovom súbore `package.json` môžeme neskôr všetko zmeniť. 
    > Na publikovanie rozšírení cez VS Code marketplace musíte mať vytvorené Windows Live konto. Účet si vytvoríte na 
stránke [https://signup.live.com/][9]. Alebo sa necháte unášať linkami na stránke s prihlásením. :)

6. A áno, určite chceme inicializovať `git` repository. Keď už sa rozhodneme rozšírenie publikovať na Github alebo 
nie, určite chceme verzovat svoj kód.

7. V aktuálnom priečinku (v našom prípade `c:\dev\text` nám vznikne nový priečinok kde sa nachádza nás vygenerovaný projekt)

## Vytvárame rozšírenie

Neviem aký editor používate vy, ale ja som si VS Code veľmi obľúbil, a keďže preň píšeme rozšírenie použijeme ho aj 
jeho vytvaranie/ladenie. Predpokladám že konzolu máme ešte stále otvorenú, tak zadáme príkaz ktorým sa nám do editora 
načíta obsah aktuálneho priečinka.

`code .`
 
(Áno, ta bodka na konci je dôležitá, a určuje aktuálny priečinok)

**Tak a môžete rozšírenie začať vytvárať ...**

> Ak dovolíte nebudem tu popisovať už nič viac. Funkčnosť rozšírenia je len a len na vás.

## Zopár tipov.

1. Vo VS Code môžete bez problémov `debugovať` dane rozšírenie. Cez `F5` spustite projekt v debug režime. môžete si 
nastaviť breakpointy, krokovať, a iné bežne činnosti vývojára.
 
![Breakpoint](/assets/posts/2016/20160222_02_Breakpoint.png){: class="img img-responsive"}

2. Testovanie rozšírenia prebieha tiež vo VS Code, ale je spustený v špeciálnom režime. Tzv. 'Extension Development Host'

3. Aj keď samotný vývoj rozšírenia bol relatívne bez problémov, v čase publikovania som dostával kompilačné chyby 
typescriptu, že nevie nájsť ten a ten modul.  Následne som zistil že ak importujem do svojej triedy *externú závislosť* 
nainštalovanú cez `npm`, musím ju importovať cez `require`, ak importujem závislosť z môjho projektu použijem bežný `import`. 

{% highlight typescript %}
import DiacriticsAdder from './diacriticsAdder';
import * as vscode from 'vscode';

var fs = require('fs');
var DiacriticsRemover = require('diacritics');
{% endhighlight %}

> Ešte si musím upratať v hlave, ako to je stými `import`, `require`, `typecriptom`, `ES5`, a `ES6` modulmi. Možno 
som robil chybu niekde ja.


4. Ak by ste potrebovali zistiť cestu kde sa rozšírenie nachádza v už keď je nainštalované (napríklad z dôvodu že ste 
do rozšírenia pribalili rôzne assets) zistíte to priamo v aktivačnej metóde daného rozšírenia, a to z kontektu:
{% highlight typescript %}
// this method is called when your extension is activated
// your extension is activated the very first time the command is executed
export function activate(context: vscode.ExtensionContext) {       
    var path = context.extensionPath;
    .
    .
}    
{% endhighlight %}

5. Chybu s nepribalenými node_modules som zistil až za behu, ak som si rozšírenie nainštaloval z Marketplace. IDE mi oznámilo 
len že nemá handling pre môj zvolený command. a nič viac. Ako postupovať v tomto prípade? Chvíľku mi trvalo, kým mi docvaklo, že `VS
Code` je postavené na technológií  `Electron`, a tam predsa sú integrované developer tools. :) Takže `Help -> Toggle Developer tools` 
nám zapne vývojársku konzolu takú ako poznáme s prehliadača Google Chrome, s ňou konzolu, a aj všetky chyby.     

![Breakpoint](/assets/posts/2016/20160222_07_DevTools.png){: class="img img-responsive"}

## Publikujeme

Ak sme úspešne odladili naše rozšírenie, prichádza na rád publikovanie do [Visual Studio Code Marketplace][8]. Ak si to 
pravdaže želáme. Samozrejme to nemusíte robiť, stačí že si vytvoríte lokálny balíček pre svoje vlastne internet použitie 
vo firme.

Na vytvorenie balíčka použijeme nástroj `vsce` čiže **VSCode Extension Manager**, ktorý sme si vyššie nainštalovali.  

Môžeme si vybrať dve cesty.

1. Chceme len vytvoriť balíček
2. Chceme rozšírenie publikovať aj do parketplace

V prípade ak sa rozhodneme ísť prvou variantou, nie je nič jednoduchšie. Z konzoly spustíme príkaz
  
`vsce package`
    
(Poznámka: predpokladám, že sa nachádzame v projektovom priečinku)

Ak všetko dobre pôjde, vznikne nám súbor `vsix`. Čo je naše rozšírenie. Takto vytvorené rozšírenie môžeme manuálne 
publikovať na marketplace. Stačí tam nahrať tento balíček. Nič od vás stránka vyžadovať nebude. Všetko si prečíta 
z projektového súboru `package.json`.

![Upload new item z marketplace](/assets/posts/2016/20160222_03_NewItemMarketplace.png){: class="img img-responsive"}

Ak pôjdeme variantom číslo 2. Čiže budeme chcieť aby nám nástroj `vsce` publikoval rozšírenie aj do marketplace automaticky
(a verte mi toto chceme, stačí zvýšiť verziu v projektovom súbore `package.json`, a opätovne spúšťať príkaz na publikovanie) 
 spustíme príkaz:
    `vsce publish` 
(Poznámka: predpokladám, že sa nachádzame v projektovom priečinku)

Ak tento príkaz spúšťame prvý krát budeme musieť zadať autorizačný **`Personál access tokens`**. Získate ho na stránke 
`Visual Studio Team Services`, vo `Vašom profile`, záložka `Security`, položka `Personál access tokens` a button `Add`.
Komplet postup podľa ktoré som postupoval je na stránke [vsce - Publishing Tool Reference`][10]. 

Príklad vyplneného formulára: 

![Personal access token formular](/assets/posts/2016/20160222_04_PersonalAccessTokenForm.png){: class="img img-responsive"}

Príklad vygenerovaného tokenu:

![Personal access token vygenerovane](/assets/posts/2016/20160222_05_PersonalAccessTokenGenerated.png){: class="img img-responsive"}

<br/>
Tento vygenerovaný `Personál access token` vložíme do konzoly, ak nás na to nástroj `vsce` vyzve.

<br/>
Ak všetko dobre pôjde, naše rozšírenie sa zobrazí či už v zozname [našich rozšírení][11], alebo v [zozname všetkých rozšírení][8].

![Moje rozšírenia](/assets/posts/2016/20160222_06_MojeRozsirenia.png){: class="img img-responsive"}


**Upozornenie**: Počas toho ako som sa snažil vypublikovať moje rozšírenie do marketplace bol bug nástroji `vsce` vo verzii 1.1.0. 
Dlho som pátral v čom je problém, a zistil som že do balíčka neboli pripálené závislosti balíčkov (vnorené balíčky resp. priečinky 
node_modules). Skúsil som urobiť downgrade nástroja vsce na verziu 1.0.0. Chyba sa tu neprejavovala. Bez problémov prebehla 
publikácia, nainštalovanie, a následne používanie balíčka bez problémov. V čase písania článku bola najnovšia verzia vsce 1.1.0. 
Downgrade npm balíčka som urobil nasledovne. 1. `npm uninstall vsce` 2. `npm install vsce@1.0.0` 
{:class="alert alert-warning"}


## Publikovanie - tipy a triky 

Všetky nastavenia vizuálu stránky s [detailom rozsirenia][12] sú preberané zo súboru `package.json` nášho projektu.

#### Readme.md
Súbor `Readme.md` bude kompletne prebratý z nášho projektu do detailu rozšírenia ako popis balíčka. 

#### Ikona rozšírenia
Ikonu v detaile rozšírenia nastavíme pomocou:
{% highlight json %}
    "icon": "assets/icon.png",
{% endhighlight %}

#### Farba pozadia
Pre zmenu pozadia nadpisu v detaile rozšírenia použijeme:  
{% highlight json %}
    "galleryBanner": {
        "color": "#5c2d91",
        "theme": "dark"
    },
{% endhighlight %}

#### Katgórie
Rozšírenie zaradíme do kategórií pomocou:
{% highlight json %}
    "categories": [
        "Other"
    ],
{% endhighlight %}

#### Sidebar odkazy

{% highlight json %}
    "repository": {
        "type": "git",
        "url": "https://github.com/jankohrasko2/XX.git"
    },
    "homepage": "https://github.com/jankohrasko2/XX/blob/master/README.md",
    "bugs": {
        "url": "https://github.com/jankohrasko2/XX/issues",
        "email": "janko@hrasko2.sk"
    }
{% endhighlight %}


## Moje rozšírenie
Ako príklad, alebo zdroj inšpirácie môžete použiť [moje rozšírenie][12], ktoré nájdete na GitHube.


[1]: http://brm.sk/diakritika "brm.sk/diakritika"
[2]: https://nodejs.org/en/download/stable/ "Node.js download"
[3]: http://yeoman.io/ "Yeoman"
[4]: https://www.npmjs.com/package/vsce "VSCE"
[5]: https://code.visualstudio.com/docs/extensions/example-hello-world [VS Code example hello world]
[6]: http://www.typescriptlang.org/ [Typescript]
[7]: https://marketplace.visualstudio.com/manage [Publish Extensions]
[8]: https://marketplace.visualstudio.com/#VSCode [VS Code Extensions]
[9]: https://signup.live.com/  [Vytvorenie Live uctu]
[10]: https://code.visualstudio.com/docs/tools/vscecli [vsce - Publishing Tool Reference]
[11]: https://marketplace.visualstudio.com/manage/publishers/ [Zoznam mojich rozsireni]
[12]: https://marketplace.visualstudio.com/items?itemName=MichalKrchnavy.vscode-diakritika-sk-extension [Moje rozsirenie]
[100]: {% post_url 2016-02-14-vytvorenie_vlastnej_webovej_stranky-blogu_s_verzionovanim_a_zdarma %} "vytvorenie_vlastnej_webovej_stranky-blogu_s_verzionovanim_a_zdarma"
