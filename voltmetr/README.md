# Analogově-digitální převodník s dvojí integrací

**Dlouhodobá maturitní práce** · SPŠE Ječná · 2026 · Martin Loskot

---

## O projektu

Tento repozitář obsahuje dokumentaci k maturitní práci zaměřené na návrh a realizaci **stolního digitálního voltmetru** postaveného na principu analogově-digitálního převodníku s dvojí integrací (dual-slope ADC). Přístroj měří stejnosměrné napětí v rozsahu **±25 V** s rozlišením přibližně **4 platných číslic**.

Cílem bylo postavit přesný měřicí přístroj s vysokou vstupní impedancí, odolností vůči rušení a funkcí samočinného nulování – vše na diskrétních součástkách s vlastním síťovým napájecím zdrojem.

---

## Fotografie

<p align="center">
  <img src="fotky/Přední strana.jpg" width="32%" alt="Přední strana"/>
  <img src="fotky/Zadní strana.jpg" width="32%" alt="Zadní strana"/>
  <img src="fotky/Osazení skříně.jpg" width="32%" alt="Osazení skříně"/>
</p>

---

## Princip funkce

Převod probíhá ve třech fázích:

| Fáze | Název | Popis |
|------|-------|-------|
| **T1** | Integrace | Vstupní napětí je po pevně danou dobu integrováno. Výsledný náboj na kondenzátoru je úměrný střední hodnotě vstupního napětí. |
| **T2** | Deintegrace (čtení) | Integrátor se vybíjí přesným referenčním napětím. Délka T2 je úměrná poměru U_vstup / U_ref. Mikrokontrolér měří tuto dobu a z ní vypočítá výsledek. |
| **T3** | Samočinné nulování | Integrační kondenzátor se vybije, provede se fiktivní převod nulového napětí a detekovaná chyba se odečte od dalšího výsledku. Eliminuje offsety OZ a termoelektrické vlivy. |

Digitální výstup je dán vztahem:

$$D_{OUT} = \frac{U_{AVG}}{U_{REF}} \cdot 2^n$$

---

## Blokové schéma

<p align="center">
  <img src="schémata/Blokové schéma.svg" alt="Blokové schéma"/>
</p>

---

## Schémata zapojení

<p align="center">
  <img src="schémata/Vstupní zesilovač.svg" width="48%" alt="Vstupní zesilovač"/>
  <img src="schémata/ADC.svg" width="48%" alt="ADC"/>
</p>
<p align="center">
  <img src="schémata/Napěťová reference.svg" width="48%" alt="Napěťová reference"/>
  <img src="schémata/Řídicí mikrokontroler.svg" width="48%" alt="Řídicí mikrokontrolér"/>
</p>
<p align="center">
  <img src="schémata/Napájecí zdroj.svg" width="60%" alt="Napájecí zdroj"/>
</p>

---

## Desky plošných spojů

<p align="center">
  <img src="PCB/Vstupní zesilovač.svg" width="48%" alt="PCB – Vstupní zesilovač"/>
  <img src="PCB/ADC.svg" width="48%" alt="PCB – ADC"/>
</p>
<p align="center">
  <img src="PCB/Napěťová reference.svg" width="48%" alt="PCB – Napěťová reference"/>
  <img src="PCB/Řídicí mikrokontroler.svg" width="48%" alt="PCB – Řídicí mikrokontrolér"/>
</p>
<p align="center">
  <img src="PCB/Napájecí zdroj.svg" width="60%" alt="PCB – Napájecí zdroj"/>
</p>

---

## Výsledky měření

Přesnost voltmetru byla ověřena porovnáním se dvěma školními digitálními multimetry.

| Měřené napětí (ref.) | Naměřeno voltmetrem | Absolutní chyba ΔU | Relativní chyba δU |
|---------------------:|--------------------:|-------------------:|-------------------:|
| −24,219 V | −24,492 V | −0,273 V | 1,13 % |
| −8,342 V | −8,445 V | −0,103 V | 1,24 % |
| 6,677 V | 6,834 V | +0,157 V | 2,35 % |
| 12,977 V | 12,203 V | +0,227 V | 1,89 % |
| 24,217 V | 24,654 V | +0,437 V | 1,81 % |

Absolutní chyba vykazuje lineární závislost na měřeném napětí: $\Delta U \approx 0{,}0136 \cdot U_{ref}$

Typická relativní chyba v pracovním rozsahu je **1,1 – 2,7 %**.

---

## Klíčové součástky

| Blok | Součástky |
|------|-----------|
| Přístrojový zesilovač | TL071, TL072 |
| Integrátor + komparátor | TL072, LM311 |
| Analogové přepínače | CD4051B, CD4052B, CD4053B |
| Napěťová reference | TL431ACZ + JFET proudový zdroj (J111) |
| Mikrokontrolér | ESP32 DEVKIT |
| Displej | 1602 LCD + I²C backpack PCF8574 |
| Napájení | LM7815, LM7915, LM7805, L78L08, L79L08 |

Plný kusovník je součástí [dokumentace (PDF)](DMP_Loskot.pdf).

---

**Autor:** Martin Loskot · **Vedoucí:** Ing. Jan Novotný, Ph.D. · **SPŠE Ječná, Praha 2 · 2026**
