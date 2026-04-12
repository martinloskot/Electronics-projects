# Analogově-digitální převodník s dvojí integrací

**Dlouhodobá maturitní práce** · SPŠE Ječná · 2026 · Martin Loskot

---

## O projektu

Tento repozitář obsahuje dokumentaci k maturitní práci zaměřené na návrh a realizaci **stolního digitálního voltmetru** postaveného na principu analogově-digitálního převodníku s dvojí integrací (dual-slope ADC). Přístroj měří stejnosměrné napětí v rozsahu **±25&nbsp;V** s rozlišením přibližně **4&nbsp;platných číslic**.

Cílem bylo postavit přesný měřicí přístroj s vysokou vstupní impedancí, odolností vůči rušení a funkcí samočinného nulování – vše na diskrétních součástkách s vlastním síťovým napájecím zdrojem.

---

## Fotografie

<p align="center">
  <img src="fotky/P%C5%99edn%C3%AD%20strana.png" width="70%" alt="Přední strana"/><br/>
  <em>Přední strana</em><br/><br/>
</p>
<p align="center">
  <img src="fotky/Osazen%C3%AD%20sk%C5%99%C3%ADn%C4%9B.png" width="70%" alt="Osazení skříně"/><br/>
  <em>Osazení skříně</em><br/><br/>
</p>
<p align="center">
  <img src="fotky/Zadn%C3%AD%20strana.png" width="70%" alt="Zadní strana"/><br/>
  <em>Zadní strana</em><br/><br/>
</p>

---

## Princip funkce

Převod probíhá ve třech fázích:

| Fáze | Název | Popis |
|------|-------|-------|
| **T1** | Integrace | Vstupní napětí je po pevně danou dobu integrováno. Výsledný náboj na kondenzátoru je úměrný střední hodnotě vstupního napětí. |
| | | |
| **T2** | Deintegrace (čtení) | Integrátor se vybíjí přesným referenčním napětím. Délka T2 je úměrná poměru $$\frac{U_{vstup}}{U_{ref}}$$. Mikrokontrolér měří tuto dobu a z ní vypočítá výsledek. |
| | | |
| **T3** | Samočinné nulování | Integrační kondenzátor se vybije, provede se fiktivní převod nulového napětí a detekovaná chyba se odečte od dalšího výsledku. Eliminuje offsety OZ a termoelektrické vlivy. |

<br/><em>

<p align="center">
  <img src="sch%C3%A9mata/Blokov%C3%A9%20sch%C3%A9ma/Blokov%C3%A9%20sch%C3%A9ma.svg" width="70%" alt="Blokové schéma"/><br/>
  <em>Blokové schéma</em><br/><br/>
</p>

---

### Jádro převodníku (ADC)

Detailní schéma analogově-digitálního převodníku (integrátor a komparátor).

<div align="center">
  <table><tr><td style="border: 1px solid #ccc; background: white;">
    <img src="sch%C3%A9mata/ADC/ADC%20sch%C3%A9ma.svg" width="600px" alt="ADC"/>
  </td></tr></table>
  <em>Schéma ADC</em><br/><br/>
</div>

---

## Dokumentace hardwaru

Všechna schémata a návrhy desek (PCB) jsou přehledně rozdělena do modulů v následující tabulce:

| Modul | Schéma (SVG) | Deska (PCB) |
| :--- | :---: | :---: |
| **Vstupní zesilovač** | [Odkaz](sch%C3%A9mata/Vstupn%C3%AD%20zesilova%C4%8D/Vstupn%C3%AD%20zesilova%C4%8D.svg) | [Odkaz](PCB/Vstupn%C3%AD%20zesilova%C4%8D/P%C5%99%C3%ADstrojov%C3%BD%20zesilova%C4%8D%20PCB.svg) |
| **Napěťová reference** | [Odkaz](sch%C3%A9mata/Nap%C4%9B%C5%A5ov%C3%A1%20reference/Nap%C4%9B%C5%A5ov%C3%A1%20reference.svg) | [Odkaz](PCB/Nap%C4%9B%C5%A5ov%C3%A1%20reference/Nap%C4%9B%C5%A5ov%C3%A1%20reference%20PCB.svg) |
| **Řídicí mikrokontrolér** | [Odkaz](sch%C3%A9mata/%C5%98%C3%ADd%C3%ADc%C3%AD%20mikrokontrol%C3%A9r/Sch%C3%A9ma%20desky%20ESP.svg) | [Odkaz](PCB/%C5%98%C3%ADdic%C3%AD%20mikrokontroler/%C5%99%C3%ADdic%C3%AD%20mikrokontrol%C3%A9r%20PCB.svg) |
| **Napájecí zdroj** | [Odkaz](sch%C3%A9mata/Nap%C3%A1jec%C3%AD%20zdroj/Nap%C3%A1jec%C3%AD%20zdroj.svg) | [Odkaz](PCB/Nap%C3%A1jec%C3%AD%20zdroj/Nap%C3%A1jec%C3%AD%20zdroj%20PCB.svg) |

---

## Výsledky měření

Přesnost voltmetru byla ověřena porovnáním se dvěma školními digitálními multimetry.

| Měřené napětí (ref.) | Naměřeno voltmetrem | Absolutní chyba ΔU | Relativní chyba δU |
|---------------------:|--------------------:|-------------------:|-------------------:|
| −24,219&nbsp;V | −24,492&nbsp;V | −0,273&nbsp;V | 1,13&nbsp;% |
| −8,342&nbsp;V | −8,445&nbsp;V | −0,103&nbsp;V | 1,24&nbsp;% |
| 6,677&nbsp;V | 6,834&nbsp;V | +0,157&nbsp;V | 2,35&nbsp;% |
| 12,977&nbsp;V | 12,203&nbsp;V | +0,227&nbsp;V | 1,89&nbsp;% |
| 24,217&nbsp;V | 24,654&nbsp;V | +0,437&nbsp;V | 1,81&nbsp;% |

Absolutní chyba vykazuje lineární závislost na měřeném napětí: $\Delta U \approx 0{,}0136 \cdot U_{ref}$

Typická relativní chyba v pracovním rozsahu je **1,1&nbsp;–&nbsp;2,7&nbsp;%**.

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

Plný kusovník je součástí [dokumentace (PDF)](Dlouhodob%C3%A1%20maturitn%C3%AD%20pr%C3%A1ce/DMP%20Loskot.pdf).

---

**Autor:** Martin Loskot · **Vedoucí:** Ing. Jan Novotný, Ph.D. · **SPŠE Ječná, Praha 2 · 2026**
