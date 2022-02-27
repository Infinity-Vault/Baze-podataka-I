# ***Prevođenje ER dijagrama u relacioni***

## Pravila za prevođenje binarne veze 

Veze ili poveznici iz ER modela podataka prevodit će se različito, ovisno o  kardinalitetu poveznika ili brojnosti veze

<hr>

**(1,1): (1,1)** ~ sve postaje jedna tabela, PK mi biramo **jedna tabela, jedan PK po izboru**

**(0,1): (1,1)** ~ samo tabele (za entitete), **prostiranje** ključa **iz (0,1)** u (1,1) **dvije tabele, prostiranje**

**(0,1): (0,1)** ~ poveznik postaje nova tabela, **PK** mi **biramo**, sta je relevantnije **tri tabele, jedan PK-izborno**

**(0,1): (1, N)** ~ poveznik postaje nova tabela, **PK** se uzima sa strane gdje je kardinalitatet **max 1** **tri tabele, PK iz 1**

**(1,1):(0,M) i (1,1):(1,M)** ~  poveznik ne postaje nova tabela, **PK** iz max **N** se prostire **u** tabelu gdje je max **1**,  **dvije tabele, prostiranje **

**(0,1):(0,M)** ~ poveznik postaje nova tabela, PK je kompoznitni ključ **tri tabele, kompozitni PK**

**(0,M):(0,M), (1,M):(0,M) i (1,M):(1,M)** ~ poveznik postaje nova tabela, PK je kompozitni ključ **tri tabele, kompozitni PK**

<hr>

**Veza M:N** 

Ukoliko su 2 tipa entiteta u vezi M:N, prevođenje ER dijagrama u relacioni model vrši se tako što svaka tip entiteta postane tabela i također tip poveznika između ta 2 tipa entiteta postaje novi tip entiteta (tabela). Tip poveznika koji je prešao u tip entiteta će imati kardinalitete 1:N prema tipovima entitetima s kojima je u vezi, te će se njegov naziv formirati spajanjem naziva oba tipa entiteta s kojima je u vezi. Primarni ključ šeme relacije je složeni ključ koji se sastoji od identifikatora objekata koji su u vezi.
**Tabele za oba entiteta + nova tabela za poveznik (postaje entiet i njegov primarni ključ je kompozitni ključ oba entiteta)**

- Ako je a1=1 tada je R1 egistencijalno ovisan od R2
- Ako je a2=1 tada je R2 egistencijalno ovisan od R1

### **Veza (0,1):(1,N)** 

**Nastaje zasebna tabela (relaciona šema), primarni ključ se uzima iz max 1.** 

### **Veza (1,1):(0,N) i (1,1):(1,N)** 

Veze kardinaliteta (1,1):(0,N) i (1,1):(1,N) ne postaju posebne šeme relacija. Identifikator objekta (primarni ključ) sa strane za koju je gornja granica kardinaliteta preslikavanja N postaje obilježje (spoljni ključ) šeme relacije koja odgovara objektu sa čije strane je maksimalni kardinalitet 1. 

### **Veza (1,1):(1,1)** 

Veza kardinaliteta (1,1):(1,1) i oba tipa entiteta koji u njoj učestvuju prevodimo u jednu šemu relacije (tabelu), čija su obilježja sva obilježja jednog i drugog tipa entiteta. Kandidat za ključ u ovoj šemi relacije su identifikatori jednog i drugog tipa entiteta koji su u vezi. 
**Postane sve jedna tabela, mi biramo primarni ključ (kandidati su iz oba entiteta)**

### **Veza (0,1):(0,1)**

Za vezu kardinaliteta (0,1):(0,1) kreiraju se tri šeme relacije (tabele), po jedna za svaki tip entiteta i jedna za poveznik. Obilježja u šemi relacije koja odgovaraju vezi su identifikatori objekata (entiteta) koji su u vezi i oba su kandidati za primarni ključ.
**Tri zasebne tabele, mi biramo primarni ključ iz jednog entiteta (kandidati su oba)**

### **Veza (0,1):(1,1)** 

Veza kardinaliteta (0,1):(1,1) i objekte u vezi prevodimo u dvije šeme relacije(tabele). Identifikator jednog od objekta koji su u vezi postaje obilježje i druge šeme relacije u ulozi spoljnog ključa. Spoljni ključ je identifikator entiteta sa čije strane je kardinalitet (0,1) u relacionoj šemi koja odgovara entitetu sa čije strane je kardinalitet (1,1). 
**Dvije relacione šeme, u entitet s kardinalitetom (1,1) dodajemo primarni ključ entiteta (0,1) u ulozi spoljašnjeg ključa.**

**2.4. Gerund ili agregirani objekt** (mješoviti tip objekt-veza) se posmatra na isti način kao  i odgovarajuća veza. Ukoliko veza posjeduje obilježja ona postaju obilježja šeme  relacije veze kada se veza prevodi u posebnu šemu relacije ili se uključuju u onu  šemu relacije u koju se upisuje spoljni ključ.

**2.5 Pravila za rekurzivne (unarne) veze**

**Prevođenje rekurzivnih ili unarnih veza** (unarnom se naziva veza između dva objekta  istog tipa) u relacioni model podataka zavisi od kardinalnaliteta tipa poveznika i izvodi se  kao i za druge tipove ranije opisanih binarnih veza. Kod unarne veze tipa (1:1)  parcijalnost samo na jednoj strani veze, odnosno totalnost samo na jednoj strani veze,  ne bi imalo smisla. Naime, time bi se istom tipu objekta istovremeno dopuštalo i poricalo  opcionalno učešće u vezi.

Pri prevođenju unarnih veza s obzirom da bi spoljni ključ u šemi relacije imao isti naziv  kao i primarni ključ, **potrebno je njegovo preimenovanje**

<hr>

### Pravila za objekte (entitete): 

<hr>

1. **Entitet**- entiteti postaju nove relacije.
2. Svaki **"slabi" objekt (slabi tip entiteta)** također postaje šema relacije. Obilježja objekta su obilježja šeme relacije.  Identifikator (primarni ključ) nadređenog tipa entiteta postaje jedno od obilježja  šeme relacije koja odgovara "slabom" tipu entiteta.
   npr. 
   S={ DRŽAVA(S_DRZAVA, NAZIV_D), (prema pravilu 1.) PROIZVOĐAČ(S_DRZAVA, S_PROIZVOD, NAZIV_P) (prema pravilu 2) }
   - **Strukturalna komponenta relacionog modela podataka je skup čiji  elementi su relacione šeme država i proizvođač**
   - **Integritetnu komponentu relacionog modela koji odgovara ER dijagramu  sa slike 1. čini međuralaciono ograničenje.**
     I={PROIZVOĐAČ[S_DRZAVA]⊆DRŽAVA[S_DRZAVA]}  vrijednosti atribta S_DRŽ u  ekstenziji relacione šeme DRŽAVA mogu biti samo one vrijednosti koje su već  pohranjene u ekstenziji relacione šeme PROIZVOĐAČ.
3. **Objekt superklase postaje šema relacije.** Naziv superklase postaje naziv šeme  relacije. Obilježja superklase su obilježja šeme relacije. Identifikator superklase  postaje ključ šeme relacije.
4. **Objekt podklasa također postaje šema relacije.** Naziv podklase postaje ime šeme  relacije. Obilježja podklase su obilježja šeme relacije. Identifikator superklase predstavlja ključ šeme relacije koja odgovara podklasi.

<hr>

### **Heurističke upute za projektovanje modela realnog sistema putem ER modela podataka**

<hr>

Neke od uputa za crtanje ER dijagrama na osnovu specifikacije informacijskih zahtjeva:

1. **Imenice** ukazuju na potrebu uvođenja tipova entiteta;
2. **Glagolski oblici** ukazuju na potrebu uvođenja tipova poveznika ili gerunda;
3. Fraze oblika: **bar jedan, najmanje jedan, više** i slično ukazuju na kardinalitet (brojnost) tipova poveznika ili gerunda;
4. Postojanje različitih **uloga** entiteta jednog skupa u vezama sa entitetima drugih skupova ukazuje na potrebu uvođenja više tipova poveznika između različitih tipova entiteta;
5. **Veze između entiteta jednog skupa** ukazuju na potrebu uvođenja rekurzivnog tipa poveznika;
6. Vremensko **prethođenje** entiteta jednog skupa u odnosu na entitete nekog drugog skupa, ukazuje na egzistencijalnu zavisnost entiteta drugog stupa of entiteta prvog skupa i potrebu uvođenja minimalnoga kardinaliteta a1=1;
7. Potreba takvog **selektivnog** povezivanja entiteta tri ili više skupova, kod kojeg u vezi mogu učestvovati samo entiteti, koji su već u nekakvoj drugoj vezi sa entitetima jednog (ili više) drugih skupova, ukazuje na neophodnost korištenja gerunda, kao modela tih drugih veza;
8. Postojanje entiteta, jednog skupa, sa **specifičnim osobinama** ili **sa specifičnim vezama** sa entitetima drugih skupova, ukazuje na potrebu uvođenja IS_A hijerarhije;
9. Postojanje entiteta sa **istim ulogama**, u okviru dva različita skupa entiteta, ukazuje na potrebu uvođenja kategorije;
10. Svaki **atribut** ili **obilježje** može pripadati samo jednom tipu entiteta ili samo jednom tipu poveznika;
11. Tip entiteta i poveznika sadrži samo ona obilježja skupa entiteta ili skupa poveznika koja su bitna za realizaciju **ciljeva** informacionog sistema koji se gradi