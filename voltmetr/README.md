# Analogově-digitální převodník s dvojí integrací

**Dlouhodobá maturitní práce** · SPŠE Ječná · 2026 · Martin Loskot

---

## O projektu

Tento repozitář obsahuje dokumentaci k maturitní práci zaměřené na návrh a realizaci **stolního digitálního voltmetru** postaveného na principu analogově-digitálního převodníku s dvojí integrací (dual-slope ADC). Přístroj je schopen měřit stejnosměrné napětí v rozsahu ±25 V s rozlišením přibližně 4 platných číslic.

Cílem bylo postavit přesný měřicí přístroj s vysokou vstupní impedancí, odolností vůči rušení a funkcí samočinného nulování – vše na diskrétních součástkách s vlastním síťovým napájecím zdrojem.

---

## Princip funkce

Převod probíhá ve třech fázích:

| Fáze | Název | Popis |
|------|-------|-------|
| **T1** | Integrace | Vstupní napětí je po pevně danou dobu integrováno. Výsledný náboj na kondenzátoru je úměrný střední hodnotě vstupního napětí. |
| **T2** | Deintegrace (čtení) | Integrátor se vybíjí přesným referenčním napětím. Délka T2 je úměrná T1 a poměru U_vstup / U_ref. Mikrokontrolér měří tuto dobu a z ní vypočítá výsledek. |
| **T3** | Samočinné nulování (autozero) | Integrační kondenzátor se vybije, provede se fiktivní převod nulového napětí a detekovaná chyba se odečte od dalšího výsledku. Eliminuje offsety OZ a termoelektrické vlivy. |

Digitální výstup je dán vztahem:

```
D_OUT = (U_AVG / U_REF) · 2^n
```

---

## Blokové schéma

```
┌──────────────┐     ┌────────────────────────┐     ┌──────────────────┐
│  Napěťová    │────▶│  Analogově-digitální   │◀────│ Vstupní          │
│  reference   │     │  převodník (dual-slope)│     │ přístrojový      │
└──────────────┘     └──────────┬─────────────┘     │ zesilovač        │
                                │ ▲                  └──────────────────┘
                                ▼ │
                     ┌──────────────────────┐        ┌──────────────────┐
                     │  I²C převodník       │◀──────▶│  Mikrokontrolér  │
                     │  logické úrovně      │        │  ESP32           │
                     └──────────┬───────────┘        └──────────────────┘
                                │
                                ▼
                     ┌──────────────────────┐
                     │  Displej 1602 LCD    │
                     └──────────────────────┘
```

Napájení všech bloků zajišťuje vlastní síťový zdroj (230 V → ±15 V / 5 V).

---

## Klíčové součástky

| Blok | Součástky |
|------|-----------|
| Přístrojový zesilovač | TL071, TL072 (diskrétní zapojení) |
| Integrátor + komparátor | TL072, LM311 |
| Analogové přepínače | CD4051B, CD4052B, CD4053B |
| Napěťová reference | TL431ACZ + JFET proudový zdroj (J111) |
| Mikrokontrolér | ESP32 DEVKIT |
| Displej | 1602 LCD, žluto-zelené podsvícení, I²C backpack PCF8574 |
| Napájení | LM7815, LM7915, LM7805, L78L08, L79L08 |

Plný kusovník je součástí [dokumentace (PDF)](DMP_Loskot.pdf).

---

## Výsledky měření

Přesnost voltmetru byla ověřena porovnáním se dvěma školními digitálními multimetry (HP34401A třída).

| Měřené napětí (ref.) | Naměřeno voltmetrem | Absolutní chyba ΔU | Relativní chyba δU |
|----------------------|--------------------|--------------------|-------------------|
| −24,219 V | −24,492 V | −0,273 V | 1,13 % |
| −8,342 V | −8,445 V | −0,103 V | 1,24 % |
| 0 V (blízko nuly) | −0,021 V | −0,004 V | 24,7 % |
| 6,677 V | 6,834 V | +0,157 V | 2,35 % |
| 12,977 V | 12,977 V | +0,227 V | 1,89 % |
| 24,217 V | 24,654 V | +0,437 V | 1,81 % |

> Chyba blízko nuly (řádek 0,02 V) je způsobena rozlišením přístroje, nikoliv systémovou chybou.  
> Absolutní chyba vykazuje lineární závislost na měřeném napětí: **ΔU ≈ 0,0136 · U_ref**

Typická relativní chyba v pracovním rozsahu je **1,1 – 2,7 %**.

---

## Fotografie

| Přední strana | Zadní strana | Osazení skříně |
|:---:|:---:|:---:|
| ![Přední strana](fotky/P%C5%99edn%C3%AD%20strana.jpg) | ![Zadní strana](fotky/Zadn%C3%AD%20strana.jpg) | ![Osazení skříně](fotky/Osazen%C3%AD%20sk%C5%99%C3%ADn%C4%9B.jpg) |

---

## Schémata

| Blok | Schéma |
|------|--------|
| Vstupní zesilovač | ![](schémata/Vstupní%20zesilovač.svg) |
| Analogově-digitální převodník | ![](schémata/ADC.svg) |
| Napěťová reference | ![](schémata/Napěťová%20reference.svg) |
| Řídicí mikrokontrolér | ![](schémata/Řídicí%20mikrokontroler.svg) |
| Napájecí zdroj | ![](schémata/Napájecí%20zdroj.svg) |

---

## Desky plošných spojů (PCB)

| Blok | PCB |
|------|-----|
| Vstupní zesilovač | ![](PCB/Vstupní%20zesilovač.svg) |
| Analogově-digitální převodník | ![](PCB/ADC.svg) |
| Napěťová reference | ![](PCB/Napěťová%20reference.svg) |
| Řídicí mikrokontrolér | ![](PCB/Řídicí%20mikrokontroler.svg) |
| Napájecí zdroj | ![](PCB/Napájecí%20zdroj.svg) |

---

## Struktura repozitáře

```
/
├── README.md
├── DMP_Loskot.pdf        # Kompletní dokumentace práce
├── fotky/                # Fotografie hotového přístroje
├── schémata/             # Schémata zapojení (SVG)
├── PCB/                  # Desky plošných spojů (SVG)
└── firmware/             # Firmware pro ESP32 (bude přidán)
```

---

## Autor a vedení

- **Autor:** Martin Loskot, třída E4
- **Vedoucí práce:** Ing. Jan Novotný, Ph.D.
- **Škola:** SPŠE Ječná, Praha 2
- **Rok:** 2026
