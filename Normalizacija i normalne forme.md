## Normalizacija i normalne forme


Normalizacija - proces koji koristimo da optimiziramo i organizujemo bazu podataka i podatke koji se nalaze u njoj. Želimo da: 

- otklonimo logičke nekonzistentnosti i greške 
- smanjimo/otklonimo redundansku (ponavljanje podataka)

Normale forme: 1NF, 2NF, 3NF, 4NF, 5NF, BCNF (Boyce-Codd-ova NF)

**Normalizacija je proces provjere uslova normalnih formi i po potrebi svođenje  šeme relacije na oblik koji zadovoljava iste.**

Bitna osobina koja se očekuje od normalizacije je reverzibilnost tj. da ne smije doći do  gubitka informacija sadržanih u početnoj relaciji. Polazeći od skupa normaliziranih  relacija, mora biti moguća rekonstrukcija početne nenormalizirane relacije

Postoje sljedeće dvije tehnike normalizacije: 

1. **Vertikalna normalizacija** 
2. **Horizontalna normalizacija**

**Vertikalna normalizacija** je postupak kojim se proizvoljna nenormalizirana šema  relacije transformira u skup manjih i normaliziranih šema relacija. Vertikalna normalizacija zasniva se na operacijama **projekcije i prirodnog spajanja**.

**Horizontalnom normalizacijom** relacija se rastavlja na podskupove n-torki – fragmente relacije koji zadovoljavaju određene uslove. Horizontalna normalizacija  zasniva se na operacijama **selekcije i unije**.

Postoje sljedeće **dvije varijante vertikalne normalizacije:**

- normalizacija dekompozicijom,  
- normalizacija sintezom

**Normalizacija dekompozicijom** započinje od proizvoljne nenormalizirane relacione  šeme i izvodi se u koracima. Svakim korakom normalizacije relaciona šema prevodi se u  višu normalnu formu, tako da se polazni skup obilježja dijeli u dva skupa i od svakog  formira posebna relaciona šema. Svaki korak normalizacije mora biti reverzibilan. Uslov koji mora biti ispunjen da bi dekompozicija bila reverzibilna glasi: **Dekompozicija relacione šeme P na relacione šeme R i S je reverzibilna ako su  zajednička obilježja u relacionim šemama R i S kandidat za ključ u bar jednoj od  ove dvije šeme**

**Normalizacija sintezom** započinje od skupa obilježja i od skupa zavisnosti zadatih na  tom skupu obilježja. Postupak se ne izvodi u koracima već se direktno formiraju relacione  šeme koje ispunjavaju uslove definirane normalnim formama

U kontekstu vertikalne normalizacije definirano je **šest normalnih formi (NF)** relacionih šema: 1NF, 2NF, 3NF, 4NF, 5NF, BCNF (Boyce-Codd-ova NF)

<hr>

**1. Normalna Forma - 1NF**

<hr>

**Relacija R** je u prvoj normalnoj formi 1NF **akko** su vrijednosti svih njenih atributa **atomske/ atomarne**. Dakle, u jednom redu- za jedan atribut može biti samo jedna informacija. 

<u>npr.</u>

| STUDENT | GODINE |  PREDMET   |
| :-----: | :----: | :--------: |
| Mrijana |   20   |  MM3, PR3  |
|  Emin   |   21   |    PR2     |
|  Anela  |   22   | Statistika |

**TABELA NIJE U 1NF JER U JEDNOM REDU POSTOJE DVIJE INFORMACIJE, MM3 I PR3.**

**Normalicijom dobijemo**

| STUDENT | GODINE |  PREDMET   |
| :-----: | :----: | :--------: |
| Mrijana |   20   |    MM3     |
| Mirjana |   20   |    PR3     |
|  Emin   |   21   |    PR2     |
|  Anela  |   22   | Statistika |

**TABELA JESTE U 1NF**

<hr>

**2. Normalna forma - 2NF** 

<hr>

**Relacija R** je u drugoj normalnoj formi **akko** je u **1NF** i ako svi njeni neključni atributi u potpunosti funkcionalno zavise od primarnog ključa. Pomoću ove forme ćemo također riješiti problem redundanse koji se može pojaviti u 1NF. 

primarni ključ (student, predmet)

| STUDENT | GODINE |  PREDMET   |
| :-----: | :----: | :--------: |
| Mrijana |   20   |    MM3     |
| Mirjana |   20   |    PR3     |
|  Emin   |   21   |    PR2     |
|  Anela  |   22   | Statistika |

**TABELA NIJE U 2F JER POSTOJI NEKLJUČNI ATRIBUT (ATRIBUT GODINE) KOJI SAMO FUNKCIONALNO ZAVISE OD STUDENTA ALI NE I PREDMETA.  **

| STUDENT | GODINE |
| :-----: | :----: |
| Mrijana |   20   |
|  Emin   |   21   |
|  Anela  |   22   |

Sada smo dvije zasebne tabele. Napravili smo zasebnu tabelu STUDENT i GODINE gdje atribut GODINE u potpunosti funckionalno zavise od studenta. 

| STUDENT |  PREDMET   |
| :-----: | :--------: |
| Mirjana |    PR3     |
| Mrijana |    MM3     |
|  Emin   |    PR2     |
|  Anela  | Statistika |

Napravili smo zasebnu tabelu STUDENT i PREDMET gdje atribut PREDMET u potpunosti funkcionalno ovisi o primarnom ključu - STUDENT. 

2NF zahtijeva da svaki stupac tabele koji nije dio primarnog ključa bude potpuno funkcionalno ovisan o cijelom primarnom ključu, a ne samo o dijelu ključa. Ovo pravilo se primjenjuje kad imate primarni ključ koji se sastoji od više od jednog stupca. Na primjer: R (ID narudžbe, ID proizvoda, Naziv proizvoda) Dizajn relacione šeme R narušava drugu normalnu formu, jer je Naziv Proizvoda ovisan o polju ID_proizvoda, ali nije o polju ID_narudžbe. Iz tabele morate ukloniti atribut Naziv proizvoda. On pripada drugoj tabeli (Proizvodi)

**TABELA JESTE U 2NF**

<hr>

**3. Normalna forma - 3NF**

<hr>

**Relacija R** je u trećoj normalnoj formi 3NF **akko** je u **2NF** i ako su svi njeni neključni atributi **netranzitivno zavise** od primarnog ključa. 

| STUDENT ID# | IME STUDENTA# |   GRAD   | DATUM ROĐENJA | POŠTANSKI BROJ |
| :---------: | :-----------: | :------: | :-----------: | :------------: |
|   IB1616    |     Amar      |  Mostar  |  16.12.1999   |     88000      |
|   IB1818    |     Emma      | Sarajevo |  21.08.2000   |     71000      |

**TABELA NIJE 3NF JER POSTOJI NEKLJČNI ATRIBUT (GRAD) KOJI ZAVISI OD DRUGOG NEKLJUČNOG ATRIBUTA (POŠTANSKI BROJ)**

| STUDENT ID# | IME STUDENTA# | DATUM ROĐENJA | POŠTANSKI BROJ |
| :---------: | :-----------: | :-----------: | :------------: |
|   IB1616    |     Amar      |  16.12.1999   |     88000      |
|   IB1818    |     Emma      |  21.08.2000   |     71000      |

**Izostavili smo neključni atribut - Grad koji zavisi od drugog neključnog atributa - Poštanski broj**

| POŠTANSKI BROJ# |   GRAD   |
| :-------------: | :------: |
|      88000      |  Mostar  |
|      71000      | Sarajevo |

**Napravili smo još jednu tabelu s atributom grad gdje je sada atribut poštanski broj postao primarni ključ**

Međutim, u ovakvim slučajevima novi entitet Poštanski broj i Grad nam ne daju nikakve značajne informacije, odnosno, ne zadovoljaju uslove za kreiranje entiteta. Ne daju nam relevantne informacije o recimo svim gradovima u BiH (biće zabilježeni samo gradovi u kojima žive studenti), poštanski brojevi se gotovo nikad ne mijenjaju. U ovakvim slučajevima je moguće zanemariti tranzitivnost atributa. 

Relacija formalno nije u trećoj normalnoj formi ali se smatra da jeste jer se (neće) desiti anomalije brisanja editovanja i dodavanja. Mada možemo kreirati novu tabelu.

**TABELA JESTE U 3NF**

Treća normalna forma zahtijeva da svaki stupac koji nije dio primarnog ključa bude ovisan o cijelom primarnom ključu i da ti stupci neključnih atributa ne budu ovisni jedan o drugome. Proizvod (ID proizvoda, Naziv, SRP, Popust),  gdje SRP predstavlja predloženu prodajnu cijenu (suggested retail price-SRP) • Popust je potrebno premjestiti u drugu tabelu, gdje postoji ključ zajedno sa SRP. F={ Id_proizvod→Naziv, SRP, Popust SRP→Popust} Proizvod (ID proizvoda, Naziv, SRP).

<hr>

**Boyce-Codd-ova normalna forma - BCNF**

<hr>
**Relacija R** je u **BCNF** ukoliko su sve **determinante** ujedino i **kandidati za ključ**. Relacija R je u BCNF ukoliko kada postoji netrivijalna zavisnost X -> X (Y nije podskup X), tada je X nadključ relacije R.

**Determinanta** je atribut u relaciji R, prost ili složen, od koga neki drugi atribut u relacij u potpunosti funkcionalno zavisi.

<u>**Uslovi za primjenu BCNF:**</u>

- postoji više kandidata za ključ
- najmanje dva od njih moraju biti složeni
- postoje zajednički atributi među kandidatima za ključeve

**U PRAKSI IZUZETNO RIJETKO!**

npr. 

R(A, B, C,D) , **FZ**(Funkcionalna zavisnost)

FZ: A-> B, C, D   --> jeste BCNF jer iz A proizilaze ostali atributi

FZ: BC-> AD --> jeste BCNF jer imamo sve atribute koji se nalaze u relaciji

FZ: D->B --> nije BCNF jer imamo atribute D i B ali nemamo atribute A i C.  NORMALIZACIJOM: 

Kreiramo dvije relacije, R2(D,B) -> iz funkcionalne zavisnosti, a R1 - prepisujemo ono što je s lijeve strane relacije koja nam "smeta" (gledamo D), s lijeve strane je A i C (B je s desne -iz funkcionalne zavisnosti) i prepisujemo D, pa slijedi R1(A, C, D).  --> Sada jeste BCNF 

<hr>

**4. Normalna forma**

<hr>

**Relacija R** je u **4NF akko** je u **3NF** i **nema višeznačne zavisnosti među atributima**. 

<u>**Višeznačna zavisnost:**</u>

R<X,Y, Z> X višeznačno određuje Y (Y zavisi od X, ali ne od Z)  **Uzrok redundanse!**

<hr>

**5. Normalna forma**

<hr>

**5NF eliminiše kružne zavisnosti (join dependencies) između entiteta!**



<hr>

Sveto pravilo: **NE DVA ENTITETA U ISTU RELACIJU tj. ne dva objetka u istu tabelu!!**







































