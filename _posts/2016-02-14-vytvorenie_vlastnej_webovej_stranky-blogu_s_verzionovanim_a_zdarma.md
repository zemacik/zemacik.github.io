---
layout: blogpost
type: post
title: "Vytvorenie vlastnej webovej stránky / blogu s verzovaním (SK)"
description: "Vytvorenie vlastnej webovej stránky / blogu s verzovaním"
date: 2016-02-14
categories:
- Jekyll
tags: [github, jekyll, tutorial]
published: true
---

Celkom nedávno sa mi poradilo rozbehnúť môj blog, a veľmi rád by som sa s vami podelil ako som to docielil.

Nechcel som použiť ťažkopádny moloch menom Wordpress. Človek sa on musí starať, t.j. kontrolovať či stránka beží, aktualizovať, dávať pozor aká aktualizácia nám rozbije zásuvné moduly a pod. A nechcel som aby bola platforma mojím pánom. Miesto toho som použil generátor Jekyll a platformu `Github pages`. Na "Github pages" môžete hosťovať svoju stránku úplne zdarma. [Ale o tom trošku neskôr.][100]

## Takže čo je to ten Jekyll?
Je to generátor statických stránok. Predstavte si že máme sériu šablón t.j. textových súborov, (ktoré v našom prípade budeme hosťovať na Githube) a potom z nich pomocou nášho nástroja Jekyll vygenerujeme kompletnú štruktúru statickej webovej stránky (čiže: HTML, CSS, JS a obrázkov)

## Prečo jekyll?
 Statických generátorov stránok existuje mnoho. Ja som zvolil Jekyll pretože ho priamo podporuje platforma Github pages. Jekyll môžete rozchodiť aj u seba lokálne na počítači, poprípade hosťovať u svojho poskytovateľa, ale o tom možno niekedy inokedy. Ja osobne fungujem tak, že som si odladil šablóny, a teraz komitujem nové šablóny priamo na github, kde ak nastane chyba pri generovať mojej statickej stránky, je mi doručený email.

 Na začiatku, kým si všetko odladíte, bude vám tých mailov choď viac.


## Výhody
- HTML stránky sú veľmi rýchle
- Statické stránky sú bezpečné (samozrejme pokiaľ máme dobre zabezpečený server)

## Nevýhody

- Statické stránky sú statické, asi ťažko tam pridáme akýkoľvek formulár na zber údajov. Čo ale môžeme, je embedovat časti stránok ako [Google forms][12], alebo [wufoo][11].
- Nie je úplne vhodný na firemné stránky, keďže asi nie každý člen teamu bude ochotný sa učiť pracovať s Gitom

## Ako začať?
Samozrejme prečítaním Jekyll dokumentácie :). Ale týmto spôsobom som ja nešiel. Miesto toho som si našiel na githube zaujímavú už hotovú šablónu (git repozitár [poole][2]) a upravil ju podľa svojich potrieb.

Ja som pre vás pripravil upravenú verziu, (Nájdete ju samozrejme tiež na githube repozitár [gihubpages-emptytemplate][1]). Si môžete jednoducho forknut (urobiť kópiu vo svojom účte) a upraviť.

## Čo budeme potrebovať
1. V prvom rade si vytvorte účet na Githube.
2. Následne si vytvorte, alebo forknite repozitár, ktorý som spomínal vyššie. (Či už [poole][2], alebo [gihubpages-emptytemplate][1])
3. Premenujte forknutý repozitár podľa vášho účtu, tak že na koniec pridáte `.github.io` na koniec. Takže napríklad ak je váš login jankohrasko2, nový repozitár sa bude volať `jankohrasko.github.io`
4. Počkať pár minút, a otvoriť si vo webovom prehliadači stránku z adresou ktorú ste si vytvorili, v našom prípade `http://jankohrasko2.github.io`

<br />
![Skrátene](/assets/posts/2016/20160214_01_postup.gif){: class="img img-responsive"}
<br />

## Popis šablóny
v prípade že ste išli cestou naklonovania existujúceho repozitára, základné rozloženie je nasledovné:
![Skrátene](/assets/posts/2016/20160214_02_rozloznie_repository.png){: class="img img-responsive" }
<br />

Keď spustíte Jekyll, vytvorí priečinok menom `_site` so statickým obsahom vo vnútry. Každý priečinok v repozitáre bude skopírovaný do priečinka `_site`, pokiaľ neobsahuje na začiatku názvu podtrhovnik (napr. "_toto-je-ignorovane").

Súbory vo formáte Markdown budú automaticky pretransformované do HTML.

Najdôležitejší súbor celého projektu je `config.yml`. Je to súbor vo formáte YAML, a obsahuje konfiguráciu nášho Jekyll projektu.

Definujeme v ňom:

- názov našej webstránky, autora, popis, poprípade kontakt
- formát markdown šablón
- akým spôsobom budú vytvárané permanentné linky na príspevky blogu
- formát stránkovania blogu
- a mnoho iného (viď. [dokumentácia][10])

Priečinky `_includes` a `_layouts` obsahujú Liquid šablóny, z ktorých nakoniec vznikne naša vygenerovaná statická stránka. `Liquid` nám pridáva dynamický obsah, do našich statických stránok.

Priečinok `_posts` obsahuje všetky príspevky blogu vo formáte `Markdown`. Github pages používajú kramdown syntax pre Markdown.

> Poznámka: Ako editor markdown súborov môžete použiť vstavaný editor na githube, alebo použiť niektorý z nástrojov na internete na editáciu markdown súborov, ja osobne používam [Visual Studio Code][8]. (To samozrejme mušte mať naklonovaný repozitár na lokálnom disku v počítači ktorý používate)

Súbor `index.html` obsahuje úvodnú stránku blogu.

Iné statické stránky vytvoríme, jednoducho ako súbory v daného repozitára, ako je v našom prípade napríklad `about.md`. Tento súbor bude tak isto pretransformovaný do HTML, a skopírovaný do priečinka `_site`, čiže dostupný na našej stránke.

**Upozornenie**: Veľmi doležité pri práci s jekyll je, že každý súbor musí byť uložený vo formáte `UTF8 bez popisnej hlavicky` reps. `UTF8 without BOM`, alebo ešte inak `UTF8 without Signature`
{:class="alert alert-warning"}


<!--# Prisposobenie stranky-->

## Použitie vlastnej domény

Ak už vlastnú doménu máte (napríklad. jankohrasko2.sk) a chcete aby vaša novo vzniknutá stránka bola prístupná z tejto adresy, musíte vytvoriť CNAME záznam v DNS konfigurácii svojej domény

> www.jankohrasko2.sk.                    CNAME	jankohrasko2.github.io.

a následne vytvoriť v repozitáre súbor s menom `CNAME` do ktorého vložíte názov vašej novo zvniknutej stránky. Či už je to `www.jankohrasko2.sk` alebo `jankohrasko2.github.io`.  

> www.jankohrasko2.sk

Pre bližšie informácie si môžete prečítať dokumentáciu o [nastavení na github pages][3].

## Ďalšie zdroje, a odkazy
- [Jekyll dokumentácia][4]
- [Github pages][5]
- [Pripravený repozitár s Jekyll šablónou][1]
- [Kramdown][6] dokumentácia (Markdown parser a konvertor používaný v githup pages)
- [jankohrasko2.github.io][7] - príklad forknutej a nasadenej Jekyll šablóny
- [Visual Štúdio Code][8]
- [Liquid markup dokumentácia][9]




[1]: https://github.com/zemacik/gihubpages-emptytemplate "gihubpages-emptytemplate"
[2]: https://github.com/poole/poole "poole"
[3]: https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/ "nastavení na github pages"
[4]: https://jekyllrb.com/docs/home/ "Jekyll dokumentácia"
[5]: https://pages.github.com/ "Github pages"
[6]: http://kramdown.gettalong.org/documentation.html "Kramdown"
[7]: https://jankohrasko2.github.io/ "jankohrasko2.github.io"
[8]: https://code.visualstudio.com/ "Visual Štúdio Code"
[9]: http://liquidmarkup.org/ "Liquid markup dokumentácia"
[10]: http://jekyllrb.com/docs/configuration/ "Jekyll konfigurácia"
[11]: http://www.wufoo.com/ "wufoo"
[12]: https://www.google.sk/intl/sk/forms/about/ "Google forms"
[100]: {% post_url 2016-02-15-pouzivame_generator_jekyll_na_lokalnom_pocitaci %} "Pouzitie na lokalnom PC"