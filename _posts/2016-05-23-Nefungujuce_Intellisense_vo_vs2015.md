---
layout: blogpost
type: post
title: "Nefungujúce intellisense vo Visual Studio 2015 (SK)"
description: "Nefungujúce intellisense vo Visual Studio 2015"
date: 2016-05-23
categories:
- Visual Studio
tags: [IDE, Tip]
published: true
canshare: true
comments: true
---

Zopár dní dozadu som riešil problém s Visual Studio 2015, kde mi z ničoho nič prestal fungovať intellisense v Xamarin.Forms projekte. 

Keďže problém sa mi podarilo vyriešiť až po pár hodinách, kde som vyskúšal už asi všetko čo sa dalo, no a predsa len ostávala jedna možnosť, ešte pred preinštalovaním celého IDE :) alebo minimálne Xamarinu.

Takže, keď budete riešiť podobný problém, snáď vám tiež pomôže to čo mne, a to:

- zo všetkých projektových priečinkov v sollution vymažte `*.user` súbory.
- vymažte `.vs\[sollution name]\v14\.suo` súbor

Následne stačí reštartovať Visual Studio, otvoriť projekt, a intellisense by malo o5 fungovať.


