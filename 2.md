# Distribuição de Frequências — Tabela 2.1

> **n = 36 empregados**  
> Notação: $f_i$ = frequência absoluta · $f_{ri}$ = frequência relativa · $f_{ri}\%$ = frequência relativa percentual · $F_i$ = frequência acumulada

---

## (a) Estado Civil

| Estado Civil | $f_i$ | $f_{ri}$ | $f_{ri}\%$ |
|:------------|------:|---------:|-----------:|
| Solteiro    |    16 |   0,4444 |     44,44% |
| Casado      |    20 |   0,5556 |     55,56% |
| **Total**   |**36** |**1,0000**|  **100,00%**|

> A maioria dos empregados é casada (≈ 56%).

---

## (b) Região de Procedência

| Região      | $f_i$ | $f_{ri}$ | $f_{ri}\%$ |
|:-----------|------:|---------:|-----------:|
| Capital     |    12 |   0,3333 |     33,33% |
| Interior    |    11 |   0,3056 |     30,56% |
| Outra       |    13 |   0,3611 |     36,11% |
| **Total**   |**36** |**1,0000**|  **100,00%**|

> A distribuição por região é bastante homogênea, com leve predominância de "outra" (≈ 36%).

---

## (c) Número de Filhos — Empregados Casados

> Subconjunto: **n = 20** empregados casados.

| Nº de Filhos | $f_i$ | $f_{ri}$ | $f_{ri}\%$ | $F_i$ | $F_{ri}\%$ |
|:------------:|------:|---------:|-----------:|------:|-----------:|
| 0            |     4 |   0,2000 |     20,00% |     4 |     20,00% |
| 1            |     5 |   0,2500 |     25,00% |     9 |     45,00% |
| 2            |     7 |   0,3500 |     35,00% |    16 |     80,00% |
| 3            |     3 |   0,1500 |     15,00% |    19 |     95,00% |
| 5            |     1 |   0,0500 |      5,00% |    20 |    100,00% |
| **Total**    |**20** |**1,0000**|  **100,00%**|       |            |

> 80% dos casados têm até 2 filhos. A moda é 2 filhos.

---

## (d) Idade (anos)

> Amplitude total: 20 a 48 anos · Amplitude de classe: **h = 5 anos** · **n = 36**

| Classe (anos) | $f_i$ | $f_{ri}$ | $f_{ri}\%$ | $F_i$ | $F_{ri}\%$ |
|:-------------:|------:|---------:|-----------:|------:|-----------:|
| [20 \|-- 25)  |     2 |   0,0556 |      5,56% |     2 |      5,56% |
| [25 \|-- 30)  |     6 |   0,1667 |     16,67% |     8 |     22,22% |
| [30 \|-- 35)  |    10 |   0,2778 |     27,78% |    18 |     50,00% |
| [35 \|-- 40)  |     8 |   0,2222 |     22,22% |    26 |     72,22% |
| [40 \|-- 45)  |     8 |   0,2222 |     22,22% |    34 |     94,44% |
| [45 \|-- 50)  |     2 |   0,0556 |      5,56% |    36 |    100,00% |
| **Total**     |**36** |**1,0000**|  **100,00%**|       |            |

> A classe modal é **[30 \|-- 35)** com 10 empregados (≈ 28%).  
> 50% dos empregados têm menos de 35 anos (mediana na 3ª classe).

---

## Código Python utilizado

```python
import csv, io
from collections import Counter

# --- carrega os dados ---
with open("tabela2_1.csv") as f:
    rows = list(csv.DictReader(f))

n = len(rows)

# (a) Estado civil
ec = Counter(r["Estado civil"] for r in rows)

# (b) Região de procedência
rp = Counter(r["Região de procedência"] for r in rows)

# (c) Filhos dos casados
casados = [r for r in rows if r["Estado civil"] == "casado"]
filhos  = Counter(int(r["Nº de filhos"]) for r in casados if r["Nº de filhos"])

# (d) Idade — classes de amplitude 5
idades  = [int(r["Idade anos"]) for r in rows]
classes = [(20,25),(25,30),(30,35),(35,40),(40,45),(45,50)]
tabela_idade = {f"[{a}|--{b})": sum(1 for x in idades if a <= x < b)
                for a, b in classes}
```
