https://cs.wikipedia.org/wiki/Refaktorov%C3%A1n%C3%AD

## REFACTORING #E_nápad💡eNÁPAD 

**Refaktorování** je disciplinovaný [proces](https://cs.wikipedia.org/wiki/Proces_(informatika) "Proces (informatika)") provádění změn v [softwarovém](https://cs.wikipedia.org/wiki/Software "Software") [systému](https://cs.wikipedia.org/wiki/Po%C4%8D%C3%ADta%C4%8Dov%C3%BD_program "Počítačový program") takovým způsobem, že nemají vliv na vnější chování [kódu](https://cs.wikipedia.org/wiki/Zdrojov%C3%BD_k%C3%B3d "Zdrojový kód"), ale vylepšují jeho vnitřní strukturu s minimálním rizikem vnášení [chyb](https://cs.wikipedia.org/wiki/Program%C3%A1torsk%C3%A1_chyba "Programátorská chyba"). Při refaktorování se provádí malé až primitivní změny, ale celkový efekt je velký, a to v podobě čistšího, průhlednějšího a čitelnějšího kódu, kód se také lépe udržuje a rozšiřuje. Zlepšuje se také celková kvalita kódu a architektura, snižuje se počet chyb a tím i zvyšuje rychlost [vývoje](https://cs.wikipedia.org/wiki/V%C3%BDvoj_software "Vývoj software") [programu](https://cs.wikipedia.org/wiki/Po%C4%8D%C3%ADta%C4%8Dov%C3%BD_program "Počítačový program"). Refaktorování pomáhá pochopit a více si ujasnit kód, což je vhodné zejména upravování [zdrojového kódu](https://cs.wikipedia.org/wiki/Zdrojov%C3%BD_k%C3%B3d "Zdrojový kód") po někom jiném.

### Úpravy metod

[[editovat](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&veaction=edit&section=7 "Editace sekce: Úpravy metod") | [editovat zdroj](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&action=edit&section=7 "Editovat zdrojový kód sekce Úpravy metod")]

- nahradit [algoritmus](https://cs.wikipedia.org/wiki/Algoritmus "Algoritmus")
- nahradit [dočasnou proměnnou](https://cs.wikipedia.org/wiki/Lok%C3%A1ln%C3%AD_prom%C4%9Bnn%C3%A1 "Lokální proměnná") dotazem (metodou, která spočítá její hodnotu)
- nahradit metodu metodou objektu
- odstranit přiřazení parametrům
- přejmenovat metodu a přejmenovat položku – změna názvu na lepší a výstižnější
- rozdělit dočasnou proměnnou
- vložit metodu
- vložit dočasnou proměnnou
- vyjmout metodu – z dlouhé metody se vyjme část kódu, který je vložen do nové metody
- zavést vysvětlující proměnnou

### Přesouvání prvků mezi objekty

[[editovat](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&veaction=edit&section=8 "Editace sekce: Přesouvání prvků mezi objekty") | [editovat zdroj](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&action=edit&section=8 "Editovat zdrojový kód sekce Přesouvání prvků mezi objekty")]

- odstranit [prostředníka](https://cs.wikipedia.org/wiki/Prost%C5%99edn%C3%ADk_(n%C3%A1vrhov%C3%BD_vzor) "Prostředník (návrhový vzor)")
- přesunout metodu a přesunout položku – přesun do vhodné třídy
- skrýt delegáta
- vyjmout třídu – vyjme se část kódu třídy a vloží do třídy nové
- vložit třídu
- zavést cizí metodu
- zavést místní rozšíření

### Organizace dat

[[editovat](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&veaction=edit&section=9 "Editace sekce: Organizace dat") | [editovat zdroj](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&action=edit&section=9 "Editovat zdrojový kód sekce Organizace dat")]

- nahradit datovou položku objektem
- nahradit [pole](https://cs.wikipedia.org/wiki/Pole_(datov%C3%A1_struktura) "Pole (datová struktura)") objektem
- zapouzdřit soukromou položku – k přístupu k proměnné použít gettery a settery
- změnit hodnotu na odkaz
- změnit odkaz na hodnotu
- zavést [objekt null](https://cs.wikipedia.org/wiki/Null_Object "Null Object")
- zavést předpoklad

### Generalizace

[[editovat](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&veaction=edit&section=10 "Editace sekce: Generalizace") | [editovat zdroj](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&action=edit&section=10 "Editovat zdrojový kód sekce Generalizace")]

- nahradit dědičnost delegováním
- nahradit delegování dědičností
- přesunout metodu výš, přesunout položku výš – přesun do předka
- přesunout metodu níž, přesunout položku níž – přesun do potomka
- přesunout tělo [konstruktoru](https://cs.wikipedia.org/wiki/Konstruktor "Konstruktor") výš – přesun do předka
- vyjmout podtřídu
- vyjmout rodičovskou třídu – vyjmutí předka
- vyjmout [rozhraní](https://cs.wikipedia.org/wiki/Rozhran%C3%AD_(informatika) "Rozhraní (informatika)") – vyjmutí rozhraní
- vytvořit šablonovou metodu
- zrušit hierarchii

### Zjednodušení volání metod

[[editovat](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&veaction=edit&section=11 "Editace sekce: Zjednodušení volání metod") | [editovat zdroj](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&action=edit&section=11 "Editovat zdrojový kód sekce Zjednodušení volání metod")]

- nahradit chybový kód výjimkou
- nahradit konstruktor tovární metodou
- nahradit parametr explicitními metodami
- nahradit parametr metodou
- nahradit výjimku testem
- oddělit dotaz a modifikátor
- odstranit parametr
- odstranit přístupovou metodu pro zápis
- [parametrizovat](https://cs.wikipedia.org/wiki/Parametrick%C3%A9_programov%C3%A1n%C3%AD "Parametrické programování") metodu
- přejmenovat metodu a přejmenovat položku – změna názvu na lepší a výstižnější
- přidat parametr
- skrýt metodu
- zachovat celý objekt
- zapouzdřit přetypování na potomka
- zavést objekt pro parametry

### Velké programování

[[editovat](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&veaction=edit&section=12 "Editace sekce: Velké programování") | [editovat zdroj](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&action=edit&section=12 "Editovat zdrojový kód sekce Velké programování")]

- roztrhnout dědičnost
- převést procedurální návrh do objektů
- vyjmout hierarchii
- oddělit [datový model](https://cs.wikipedia.org/wiki/Datov%C3%A9_modelov%C3%A1n%C3%AD "Datové modelování") od prezentace

### Ostatní techniky

[[editovat](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&veaction=edit&section=13 "Editace sekce: Ostatní techniky") | [editovat zdroj](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&action=edit&section=13 "Editovat zdrojový kód sekce Ostatní techniky")]

- duplikovat sledovaná data
- nahradit kód typu podtřídami
- nahradit kód typu třídou
- nahradit magické číslo symbolickou konstantou
- nahradit podtřídu položkami
- nahradit vnořenou podmínku varovnými klausulemi
- nahradit podmínku [polymorfismem](https://cs.wikipedia.org/wiki/Polymorfismus_(programov%C3%A1n%C3%AD) "Polymorfismus (programování)")
- nahradit kód typu stavem nebo strategií
- odstranit příznak
- zachovat celý objekt

## Refaktorování a návrhové vzory

[[editovat](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&veaction=edit&section=14 "Editace sekce: Refaktorování a návrhové vzory") | [editovat zdroj](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&action=edit&section=14 "Editovat zdrojový kód sekce Refaktorování a návrhové vzory")]

Existuje vazba mezi refaktorováním a [návrhovými vzory](https://cs.wikipedia.org/wiki/N%C3%A1vrhov%C3%BD_vzor "Návrhový vzor"), a to taková, že vzory popisují definovaný cíl a naopak refaktorování popisuje způsob, jak se k tomuto cíli dostat.

## Podpora refaktorování

[[editovat](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&veaction=edit&section=15 "Editace sekce: Podpora refaktorování") | [editovat zdroj](https://cs.wikipedia.org/w/index.php?title=Refaktorov%C3%A1n%C3%AD&action=edit&section=15 "Editovat zdrojový kód sekce Podpora refaktorování")]

Některé postupy při refaktorování je možné přesně definovat a zcela automatizovat a dnes je již v moderních vývojových prostředích nabízena podpora při refaktorování. Technika vyjmout metodu z dlouhé metody již tedy není složitá a prakticky u něj není ani potřeba více přemýšlet, udělá jej program. Někteří si při psaní kódu ani neuvědomují, že například změna názvu proměnné je také refaktorování, které provede program, avšak dříve tato změna byla velmi náročná.