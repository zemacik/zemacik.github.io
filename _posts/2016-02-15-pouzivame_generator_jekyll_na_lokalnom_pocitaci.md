---
layout: blogpost
type: post
title: "Používame generátor Jekyll na lokálnom počítači (SK)"
description: "Používame generátor Jekyll na lokálnom počítači"
date: 2016-02-15
categories:
- Jekyll
tags: [jekyll, tutorial]
published: true
canshare: true
comments: true
---

V [predchádzajúcom príspevku][100] som popisoval ako rozbehnúť vlastnú stránku / blog postavenú na statickom generátore stránok `Jekyll`, a platforme `Github pages`. 

V článku som spomenul, že lokálne nemám generátor nainštalovaný, a používam ho metódou 'update', `commit`, `refresh`, a ak bolo niečo zlé, zistil som to až keď sa na githup pages pregenerovala celá stránka. Nebolo príliš zdĺhavé, ale určite časové zdržanie od update, po refresh stránky tam bolo.

Preto som sa rozhodol že vyskúšam si nainštalovať jekyll lokálne. Jekyll je postavený nad ruby, tak som mal obavu či to bude bez problémov fungovať. Našťastie som sa mýlil.

Na inštaláciu som použil [Chocolatey][2], je to manažér balíčkov pre windows. Niečo ako `apt-get` pre linux, alebo `npm` pre node.jš. 

Mať nainštalované 'Chocolatey' je jediná prerekvizita, aby vám dole uvedený postup fungoval.


## Ako nainštalovať Chocolatey?

1. Otvorte si príkazový riadok s právami administrátora

2. Nainštalujeme Chocolatey spustením príkazu

    `@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin`
 
3. Zatvoríme okno. Tento krok je dôležitý, aby sa nám opätovne načítali systémové premenné. A príkaz `choco` bol dostupný z konzoly.


## Ako nainštalovať Jekyll?

Postup je tak isto veľmi jednoduchý.

1. Otvorte si príkazový riadok

2. Spustíme príkaz ktorým nainštalujeme programovací jazyk `ruby`
    
    `choco install ruby -y`

3. Spustíme príkaz ktorým nainštalujeme samotný `Jekyll`

    `gem install jekyll`

4. Zatvoríme okno príkazového riadka


To je všetko, jekyll máme nainštalovaný. A ani to nebolelo, že? :)


## Vyskúšanie funkčnosti

1. Otvorte si príkazový riadok

2. Vojdeme do priečinka s našim jekyll projektom

    > Ja mám umiestnený projekt v priečinku c:\dev\jekyll\test čiže spustím `cd c:\dev\jekyll\test`
 
3. Spustíme príkaz

    `jekyll serve`

<br/>
![Postup v obrázku](/assets/posts/2016/20160215_01_jekyll_serve.gif){: class="img img-responsive"}
<br/>

Ak je jekyll schopný vygenerovať stránky, oznámi nám lokálnu webovú adresu kde si môžeme stránku prezrieť na lokálnom počítači. V našom prípade `http://localhost:4000`. Túto stránku si otvorte vo webovom prehliadači. 

> Po každom uložení editovanej šablóny v projekte, jekyll automaticky pregeneruje stránku. (Ak zmeníte súbor _config.yml, tak je vhodné ukončiť bežiaci jekyll process "CTRL+C", a spustiť ho opätovne `jekyll serve`)


<br/>

Myslím že toto som mohol používať už od začiatku a ušetriť si zopár minút času. 


[2]: https://chocolatey.org/ "Chocolatey"
[100]: {% post_url 2016-02-14-vytvorenie_vlastnej_webovej_stranky-blogu_s_verzionovanim_a_zdarma %} "Oboznamenie sa s Jekyll"
