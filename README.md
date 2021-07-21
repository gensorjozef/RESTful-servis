Zadanie implementačnej úlohy
Vytvorte RESTful servis, ktorý bude poskytovať informácie o jedlách ponúkaných v jedálni na celý týždeň. Menu s 
ponukou pre jeden deň poskytuje vo formáte xml so štruktúrou:

Poznámka. Uvedené xml je len príklad, ktorý ilustruje požadovanú štruktúru. XML dokumenty, ktorými pracuje servis 
majú elementy s rovnakými názvami a štruktúrou, odlišovať môžu len textovým obsahom a počtom elementov
POZOR dôležité!
- Resource package nazvite: rest
- Koreňový resource nazvite: menu
- Ak používate @Singleton importujte javax.inject.Singleton
- Dátové triedy vytvárajte tiež v package rest

POKYNY k odovzdaniu: Do AISu sa odovzdáva celý zozipovaný adresár rest (so všetkými súbormi, ktoré ste 
vytvorili)
Menu s ponukou pre jeden deň bude pristupné ako resource s URL menu/{den}
kde den je meno dňa v týždni. Platné mená dní sú reťazce: pondelok, utorok, streda, stvrtok, piatok, 
sobota, nedela
Jednoltivé jedlá v ponuke dňa budú prístupné ako subresoursy s URL menu/{den}/{n}
kde n je poradové číslo jedla v ponuke daného dňa, pričom jedlá sú číslované za sebou od 1.
Inicializácia: Pri štarte si aplikácia inicializuje ponuku pre každý deň v týždni, pričom pondelok bude obsahovať jediné 
jedlo s názvom gulas a cenou 3.5. Ponuka pre ostatné dni nebude obsahovať žiadne jedlá.
Pre URL ponuky dňa menu/{den} implementujte metódy:
GET pre MIME text/plain: vráti aktuálny počet jedál v menu pre daný deň.
GET pre MIME application/xml: vráti kompletné menu ako xml s horeuvedenou štruktúrou
POST pre MIME application/xml: pridá nové jedlo do ponuky pre daný deň. Akceptuje xml dokument so štruktúrou:

Metóda vráti poradové číslo nového jedla v ponuke (MIME text/plain).
Pred vložením nového jedla do zoznamu metóda overí, či sa v ponuke dňa už jedlo s daným názvom nenachádza. Ak sa 
nachádza,, nepridá ho (neurobí nič) a vráti 0. 
Pre URL jedla menu/{den}/{n} implementujte metódy:
GET pre MIME application/xml: vráti xml so všetkými informáciami o jedle s poradovým číslom n.
DELETE: odstráni jedlo s poradovým číslom n z menu pre daný deň. 
Poznámka: Po odstránení jedla sa poradové čísla jedál za ním znížia!
Servis umožňuje tiež zistiť, ktorý deň je jedlo v ponuke. Túto funkcionalitu implementujte pomocou metódy 
GET pre koreňový resource menu (MIME text/plain).
Názov jedla je zadaný ako parameter požiadavky nazov (Pomôcka @QueryParam(“nazov”) - pozri ťahák).
Metóda zistí, v ktorých dňoch sa jedlo s daným názvom nachádza v ponuke a vráti reťazec, zložený mien dní , 
oddelených medzerou, napr. streda piatok. Ak meno nie je v ponuke žiadny deň, vráti reťazec NEMAME.
Poznámka. Ak klient volá metódy pre neexistujúci resource, server by mal vrátiť null prípadne niektorý z chybových 
kódov HTTP 20* alebo 40*, (v žiadnom prípade nesmie vrátiť kód HTTP 50*
