---
header-includes:
	\usepackage[czech]{babel}
	\usepackage{a4wide}
---
# Kód
## Řešení
Kódování nebude fungovat v případě, že k je menší, nebo rovno 3.

### Zakódování
Rozdělíme vstup po (k - 2)/2 bitech. Poté posíláme vždy danou část bitů následovanou známým bitem, například 0, nebo 1, 
a toto pošleme dvakrát.

#### Příklad
Máme vstupní posloupnost bitů: 10010110; k = 10\
Rozdělíme je po (10-2)/2 = 4\
1001 a 0110\
a pošleme spolu se známým bitem (0).\
`10010100100110001100`

### Dekódování
Bity opět rozdělíme, ale tentokrát na skupiny o velikosti k. Poté si z každé skupiny vytáhneme známé bity tj. poslední 
a prostřední (k/2). Poté podle jejich kombinace zjistíme správnou posloupnost bitů, které byli poslány. Máme 
4 možnosti:\
1. Oba dva bity jsou správně.\
Správně je druhá skupina.\
2. Oba dva bity jsou negované.\
Správně je negovaná druhá skupina, všechny bity se musí znegovat.\
3. První bit je správně, druhý je špatně.\
Správně je první skupina.\
4. První bit je špatně, druhý správně.\
Správně je negovaná první skupina.

#### Příklad
Vyjdeme z příkladu nahoře a dejme tomu že nám přijde takováto posloupnost bitů.\
`1001001101`...\
Vytáhneme si kontrolní bity. {0;1}. A podíváme se do které skupiny spadají, do 3. A tudíž víme že zakódovaná posloupnost 
je shodná s první skupinou, tj. `1001`.

### Správnost
Rozeberu postupně všechny možnosti.\
1. Druhá skupina musí být správně, jelikož vzdálenost známých bitů od sebe je menší než k, konkrétně jeho polovina. 
   A tudíž pokud by nastala chyba mezi nimi musela by se nutně projevit na druhém ze známých bitů.\
2. Druhý případ je podobný prvnímu s tím rozdílem, že vše je negované, takže i druhá skupina musí být negována.\
3. Pokud je první kontrolní bit správně a druhý špatně, musela nastat chyba někde mezi nimi, a protože nastala mezi nimi 
   předchozí chyba musela nastat před prvním bitem daného bloku, konec je od začátku vzdálen přesně (k - 1). Tudíž 
   správná posloupnost bitů je ta první.\
4. U posledního případu musela chyba nastat též mezi prvním a druhým bitem, pouze s tím rozdílem, že vrátila komunikaci 
   do normálního stavu, tj. komunikace před ní byla negována. Takže správná posloupnost bitů vznikne negováním první 
	   skupiny.
