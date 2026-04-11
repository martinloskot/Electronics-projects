# Zesilovač ve třídě A — BJT (NPN, BC547C)

Jednopólový tranzistorový zesilovač ve třídě A s nastavením pracovního bodu pomocí napěťového děliče (RB1, RB2).

## Schéma zapojení

![Schéma zapojení](schéma/schéma.svg)

## Parametry obvodu

| Parametr            | Hodnota  |
|---------------------|----------|
| Napájecí napětí UCC | 10 V     |
| Klidový proud ICP   | 6 mA     |
| Pracovní bod UC     | 5 V      |
| Zesílení β (h21E)   | 400      |
| UBEP                | 650 mV   |

## Výpočet pracovního bodu

Výpočty jsou v souboru [`výpočet/zesilovač s výpočty.xlsx`](výpočet/zesilovač%20s%20výpočty.xlsx).

### Hodnoty součástek (řada E12)

| Součástka | Vypočítaná hodnota | Použitá hodnota |
|-----------|-------------------|-----------------|
| RB1       | 28,24 kΩ          | 27 kΩ           |
| RB2       | 3,68 kΩ           | 3,9 kΩ          |
| RC        | 833 Ω             | 820 Ω           |
| RE        | 75,8 Ω            | 82 Ω            |
| C1, C2    | —                 | 10 µF           |
| C3        | —                 | 100 µF          |

### Ověření pracovního bodu

| Veličina | Teorie    | Měřeno    |
|----------|-----------|-----------|
| UC       | 5,000 V   | 5,367 V   |
| URE      | 454,5 mV  | 397,1 mV  |
| UB       | 1,105 V   | 1,051 V   |
| UBE      | 650 mV    | 653,5 mV  |

Odchylka UC od 0,5 UCC: **7,3 %**

## Naměřené výsledky

| Uvst (mV) | Uvýst (mV) | Au (-)  | Rvst (kΩ) | Rvýst (Ω) |
|-----------|------------|---------|-----------|-----------|
| 50,2      | 563,1      | 11,26   | 14,34     | 1 000     |

## Návrh PCB

![PCB](PCB/zesilovač%20PCB.svg)

## Soubory

- [`schéma/`](schéma/) — schéma zapojení (KiCad EEschema)
- [`PCB/`](PCB/) — návrh plošného spoje
- [`výpočet/`](výpočet/) — Excel s výpočty pracovního bodu a měřením
