# Zesilovač ve třídě A — BJT (NPN)

Jednoduchý jednopólový tranzistorový zesilovač ve třídě A s nastavením
pracovního bodu pomocí napěťového děliče (RB1, RB2).

## Schéma zapojení

> *(doplň obrázek nebo odkaz na schéma)*

## Parametry obvodu

| Parametr            | Hodnota  |
|---------------------|----------|
| Napájecí napětí UCC | 10 V     |
| Klidový proud ICP   | 6 mA     |
| Pracovní bod UC     | 5 V      |
| Zesílení β (h21E)   | 400      |
| UBEP                | 0,65 V   |

## Výpočet pracovního bodu

Výpočty jsou v souboru [`calculations/zesilovac_s_vypocty.xlsx`](calculations/zesilovac_s_vypocty.xlsx).

Postup:
1. Volba ICP a UCC → výpočet RC, RE
2. Výpočet napěťového děliče RB1, RB2
3. Zaokrouhlení na hodnoty řady E12
4. Ověření polohy pracovního bodu

### Vypočítané a použité hodnoty (řada E12)

| Součástka | Vypočítaná hodnota | Použitá hodnota (E12) |
|-----------|-------------------|-----------------------|
| RB1       | 28,24 kΩ          | 27 kΩ                 |
| RB2       | 3,68 kΩ           | 3,9 kΩ                |
| RC        | 833 Ω             | 820 Ω                 |
| RE        | 75,8 Ω            | 82 Ω                  |

> Vybrané hodnoty E12 posunou UC mírně od ideálního středu (0,5 × UCC),
> přičemž RC byl snížen kvůli produktu děliče a báze, RE zvýšen kvůli změně poměru děliče.

## Naměřené výsledky

| IC (A)  | Uvst (V)  | Uvýst (V) | Au (-)  | Rvst (Ω)      | Rvýst (Ω)  |
|---------|-----------|-----------|---------|---------------|------------|
| 0,1 mA  | 0,049 V   | 0,524 V   | ~10,2   | ~4 256 Ω      | ~636 Ω     |
| 1 mA    | 0,050 V   | 0,327 V   | ~6,4    | ~17 183 Ω     | ~4 641 Ω   |
| bez IC  | 0,050 V   | 0,563 V   | ~11,3   | ~14 342 Ω     | ~1 000 Ω   |

### Kondenzátory

| Součástka | Hodnota |
|-----------|---------|
| C1        | 10 µF   |
| C2        | 10 µF   |
| C3        | 100 µF  |

## Soubory

- [`calculations/`](calculations/) — Excel s výpočty pracovního bodu a měřením
- [`schematic/`](schematic/) — schéma zapojení
- [`pcb/`](pcb/) — návrh plošného spoje
