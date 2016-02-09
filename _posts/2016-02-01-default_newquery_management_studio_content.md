---
layout: blogpost
type: post
title: "Predvolený obsah \"New query\" okna v SQL Server Management Studio (SK)"
description: "Ukážeme si ako si prevoliť šablónu pre nový query v management studio"
date: 2016-02-09
categories:
- SQL
tags: [sql, tools]
published: true
---

Mám pre vás jeden tip, ktorý určite trošku zefektívni vašu prácu v SQL Server management štúdiu, a ak nie tak aspoň Vám zachráni zadok.
 
Túto myšlienku mi vnukol kolega, ktorý nám takmer prepísal všetky oprávnenia v databáze, pretože zabudol WHERE podmienku v SQL dotaze.

Tak som trošku pátral, a zistil som že je možné nastaviť predvolený obsah novom "New query" okne.


### Čo ideme robiť?

Nastavíme si predvolený obsah, tak aby sme mali defaultné náš query ktorý napíšeme zabalený do transakcie, ktorá sa ukončí ROLLBACKom.
Samozrejme ak nepotrebujeme transakciu obsah jednoducho zmažeme :)

Obsah ktorý si vložíme do šablóny.

{% highlight sql %}
```sql
BEGIN TRANSACTION;

/** CONTENT HERE */

ROLLBACK TRANSACTION;
--COMMIT TRANSACTION;
```
{% endhighlight %}

### Takže ako na to?

Potrebujeme nájsť súbor so šablónou. Pre každú verziu Management studia sa súbor nachádza v inej lokalite.

Cesta pre SQL Server Management studio 2014 sa nachádza:
> c:\Program Files (x86)\Microsoft SQL Server\120\Tools\Binn\ManagementStudio\SqlWorkbenchProjectItems\Sql\SQLFile.sql

Pre ostatné verzie mysime vestu upraviť cestu:

| Verzia                     | Priečinok |
|----------------------------|-----------|
|Microsoft SQL Server 2014   |120        |
|Microsoft SQL Server 2012   |110        |
|Microsoft SQL Server 2008 R2|100        |
|Microsoft SQL Server 2008   |100        |


1. Súbor modifikujeme podľa modla svojej vôle, ja používam template uvedený vyššie  
2. Uložíme 
3. A po stlačení "New query" dostaneme nový súbor vyplnený našou šablónou 

Poznámka:
Prosím majte na pamäti že tento súbor je spoločný pre všetkých používateľov daného počítača.
