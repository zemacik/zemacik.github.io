---
layout: blogpost
type: post
title: "Podpisovanie UWP (Windows 10) aplikácie vlastným certifikátom zákazníka"
description: "Podpisovanie UWP (Windows 10) aplikácie vlastným certifikátom zákazníka"
date: 2017-03-09
categories:
- Vývoj
tags: [UWP, Metro]
published: true
canshare: true
comments: true
---


Pre klienta z oblasti poskytovania leasingu riešime aplikáciu na elektronické podpisovanie dokumentov. Zákazník si ako svoju platformu vybral Microsoft Windows, a technológiu UWP (Universal Windows Platform).

> Dolu popísaný postup je možné použiť aj pre tzv. Metro aplikácie pre Windows 8, a Windows 8.1

Keďže aplikácia nie je distribuovaná štandardne cez Microsoft Store, riešili sme problém ako aplikáciu podpísať tak, aby ju bolo možné bezpečné prevádzkovať na počítačoch klienta.


## Možnosti distribúcie aplikácie

Ešte predtým než spomeniem aké sme mali možnosti, musím napísať ako je možné dostať UWP aplikáciu na počítač používateľa. 

1. Tou prvou, je inštalácia aplikácie cez Microsoft Store. V tomto prípade je nutné aby prešla certifikačným procesom Microsoftu. Následne je aplikácia podpísaná dôveryhodným certifikátom, a sprístupnená na stiahnutie, podľa nastavení v store.

2. možnosť je prepnúť každé zariadenie do Vývojárskeho režimu (Developer mode). V tomto režime je možné do zariadenia nainštalovať akúkoľvek UWP aplikáciu. To znamená že môže byť podpísaná akýmkoľvek certifikátom. 

3. možnosť je takzvaný Sideload režim. Tento režim umožňuje do zariadenia nainštalovať aplikácie ktoré sú podpísané dôveryhodným certifikátom pre dané zariadenie.

Keďže infraštruktúra klienta musí spĺňať určité bezpečnostné kritériá, nie je možné aby boli zariadenia vo vývojárskom režime. Čiže Sideload režim, je cesta akou sme sa vydali.


![Windows developer mode](/assets/posts/2017/20170309_WindowsDeveloeprModes.png){: class="img img-responsive" style="padding: 25px;"}

<br/>
Režim zariadenia máme prepnutý, a teraz ku samotnému podpisovaniu aplikácie.
<br/>

## Podpisovanie aplikácie

Núkalo sa nám viac možností:

1. Aplikáciu budeme podpisovať naším certifikátom t.j. dodávateľskej firmy. To však znamená, že každé zariadenie kde bude naša aplikácia nainštalovaná bude musieť dôverovať certifikátu ktorým je podpísaná.

    Čo však vystavuje tieto zariadenia riziku, že ak by sa tento náš certifikát, dostal do nepovolaných rúk, podpísal nevhodnú aplikáciu, táto by mohla byť bez akýchkoľvek problémov nainštalovaná na zariadenia klienta. Čo nechceme.

2. možnosť, je podpísanie aplikácie certifikátom klienta. Keďže na podpísanie aplikácie potrebujeme certifikát s privátnym kľúčom, z rovnakých dôvodov ako v bode 1. nám klient nemohol certifikát poskytnúť. 

Rozhodli sme sa teda že aplikáciu si bude klient podpisovať sám, vo vlastnej réžii.

Od nás, ako dodávateľa odchádza release `APPX` balíčka pre každú platformu (`x86, x64, ARM`), podpísaný dočasným certifikátom, ktorý je súčasťou projektu. 

Následne, na strane klienta je nutné aplikáciu opätovne podpísať, tým správnym certifikátom.

## Postup podpísania

Teraz by som chcel spísať kroky, ktoré je nutné vykonať aby sme na strane klienta získali plnohodnotný balíček, ktorý môžeme ďalej distribuovať cez SCCM, alebo manuálne inštalovať na každé zariadenie klienta, ktoré dôveruje podpisovému certifikátu.

1. v prvom rade musíme aplikáciu rozpakovať

    `MakeAppx unpack /l /p "NasaAplikacia_x86.appx" /d "C:\NasaAplikacia"`

2. musíme zmeniť Publishera aplikácie v aplikačnom manifeste. Čiže v súbore `C:\NasaAplikacia\AppxManifest.xml` vymeníme `"CN=[STAREMENO]"` za `"CN=[NOVEMENO]"` kde NOVEMENO je názov publishera certifikátu ktorým podpisujeme.

3. následne môžeme aplikáciu opätovne zbaliť, a vytvoriť tak nepodpísaný APPX balíček.

    `MakeAppx pack /l /d " C:\NasaAplikacia" /p "C:\[NovyNazovBalicka].appx"`

4. V ďalšom ktorú aplikáciu podpíšeme našim novým certifikátom. 

    `Signtool.exe sign /a /v /fd SHA256 /f /p [HESLO CERTIFIKATU] "C:\NovyCertifikat.pfx" C:\[NovyNazovBalicka].appx`

Takže teraz máme balíček, ktorý môže klient bez problémov inštalovať na svoje zariadenia.


## Poznámka bokom

Ešte pre úplnosť by som uviedol že všetky použité nástroje ako `MakeAppx.exe`, `Signtool.exe`, `makecert.exe`, `pvk2pfx.exe`, sa nachádzajú v priečinkoch:

{% highlight json %}

"c:\Program Files (x86)\Windows Kits\10\bin\x64"
"c:\Program Files (x86)\Windows Kits\10\bin\x86" 
"c:\Program Files (x86)\Windows Kits\8.1\bin\x86" 
"c:\Program Files (x86)\Windows Kits\8.1\bin\x86" 
"c:\Program Files (x86)\Windows Kits\8.0\bin\x86" 
"c:\Program Files (x86)\Windows Kits\8.0\bin\x86" 

{% endhighlight %}

Sú súčasťou tzv. Windows Software Development Kit (SDK) pre Windows 10, 8.1, 8.

- [Windows 10 SDK](https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk)
- [Windows 8.1 SDK](https://developer.microsoft.com/en-us/windows/downloads/windows-8-1-sdk)
- [Windows 8.0 SDK](https://developer.microsoft.com/en-us/windows/downloads/windows-8-sdk)



