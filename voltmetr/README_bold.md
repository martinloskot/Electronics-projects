# Analogově-digitální převodník s dvojí integrací

**Dlouhodobá maturitní práce** · SPŠE Ječná · 2026 · Martin Loskot

------------------------------------------------------------------------

## O projektu

Tento repozitář obsahuje dokumentaci k maturitní práci zaměřené na návrh
a realizaci **stolního digitálního voltmetru** postaveného na principu
analogově-digitálního převodníku s dvojí integrací (dual-slope ADC).
Přístroj měří stejnosměrné napětí v rozsahu **±25 V** s rozlišením
přibližně **4 platných číslic**.

Cílem bylo postavit přesný měřicí přístroj s vysokou vstupní impedancí,
odolností vůči rušení a funkcí samočinného nulování -- vše na
diskrétních součástkách s vlastním síťovým napájecím zdrojem.

------------------------------------------------------------------------

## Fotografie

```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="fotky/P%C5%99edn%C3%AD%20strana.png" width="70%" alt="Přední strana"/>`{=html}`<br/>`{=html}
`<em>`{=html}Přední strana`</em>`{=html}
```{=html}
</p>
```
```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="fotky/Osazen%C3%AD%20sk%C5%99%C3%ADn%C4%9B.png" width="70%" alt="Osazení skříně"/>`{=html}`<br/>`{=html}
`<em>`{=html}Osazení skříně`</em>`{=html}
```{=html}
</p>
```
```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="fotky/Zadn%C3%AD%20strana.png" width="70%" alt="Zadní strana"/>`{=html}`<br/>`{=html}
`<em>`{=html}Zadní strana`</em>`{=html}
```{=html}
</p>
```

------------------------------------------------------------------------

## Princip funkce

Převod probíhá ve třech fázích:

  -----------------------------------------------------------------------
  Fáze                  Název                    Popis
  --------------------- ------------------------ ------------------------
  **T1**                Integrace                Vstupní napětí je po
                                                 pevně danou dobu
                                                 integrováno. Výsledný
                                                 náboj na kondenzátoru je
                                                 úměrný střední hodnotě
                                                 vstupního napětí.

  **T2**                Deintegrace (čtení)      Integrátor se vybíjí
                                                 přesným referenčním
                                                 napětím. Délka T2 je
                                                 úměrná poměru
                                                 U_vstup / U_ref.
                                                 Mikrokontrolér měří tuto
                                                 dobu a z ní vypočítá
                                                 výsledek.

  **T3**                Samočinné nulování       Integrační kondenzátor
                                                 se vybije, provede se
                                                 fiktivní převod nulového
                                                 napětí a detekovaná
                                                 chyba se odečte od
                                                 dalšího výsledku.
                                                 Eliminuje offsety OZ a
                                                 termoelektrické vlivy.
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## Blokové schéma

```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="sch%C3%A9mata/Blokov%C3%A9%20sch%C3%A9ma/Blokov%C3%A9%20sch%C3%A9ma.svg" width="70%" alt="Blokové schéma"/>`{=html}`<br/>`{=html}
`<em>`{=html}Blokové schéma`</em>`{=html}
```{=html}
</p>
```

------------------------------------------------------------------------

## Schémata zapojení

```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="sch%C3%A9mata/Vstupn%C3%AD%20zesilova%C4%8D/Vstupn%C3%AD%20zesilova%C4%8D.svg" width="70%" alt="Vstupní zesilovač"/>`{=html}`<br/>`{=html}
`<em>`{=html}Vstupní zesilovač`</em>`{=html}
```{=html}
</p>
```
```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="sch%C3%A9mata/ADC/ADC%20sch%C3%A9ma.svg" width="70%" alt="ADC"/>`{=html}`<br/>`{=html}
`<em>`{=html}Analogově-digitální převodník`</em>`{=html}
```{=html}
</p>
```
```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="sch%C3%A9mata/Nap%C4%9B%C5%A5ov%C3%A1%20reference/Nap%C4%9B%C5%A5ov%C3%A1%20reference.svg" width="70%" alt="Napěťová reference"/>`{=html}`<br/>`{=html}
`<em>`{=html}Napěťová reference`</em>`{=html}
```{=html}
</p>
```
```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="sch%C3%A9mata/%C5%98%C3%ADd%C3%ADc%C3%AD%20mikrokontrol%C3%A9r/Sch%C3%A9ma%20desky%20ESP.svg" width="70%" alt="Řídicí mikrokontrolér"/>`{=html}`<br/>`{=html}
`<em>`{=html}Řídicí mikrokontrolér`</em>`{=html}
```{=html}
</p>
```
```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="sch%C3%A9mata/Nap%C3%A1jec%C3%AD%20zdroj/Nap%C3%A1jec%C3%AD%20zdroj.svg" width="70%" alt="Napájecí zdroj"/>`{=html}`<br/>`{=html}
`<em>`{=html}Napájecí zdroj`</em>`{=html}
```{=html}
</p>
```

------------------------------------------------------------------------

## Desky plošných spojů

```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="PCB/Vstupn%C3%AD%20zesilov%C3%A1%C4%8D/P%C5%99%C3%ADstrojov%C3%BD%20zesilov%C3%A1%C4%8D%20PCB.svg" width="70%" alt="PCB – Vstupní zesilovač"/>`{=html}`<br/>`{=html}
`<em>`{=html}Vstupní zesilovač`</em>`{=html}
```{=html}
</p>
```
```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="PCB/ADC/ADC%20PCB.svg" width="70%" alt="PCB – ADC"/>`{=html}`<br/>`{=html}
`<em>`{=html}Analogově-digitální převodník`</em>`{=html}
```{=html}
</p>
```
```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="PCB/Nap%C4%9B%C5%A5ov%C3%A1%20reference/Nap%C4%9B%C5%A5ov%C3%A1%20reference%20PCB.svg" width="70%" alt="PCB – Napěťová reference"/>`{=html}`<br/>`{=html}
`<em>`{=html}Napěťová reference`</em>`{=html}
```{=html}
</p>
```
```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="PCB/%C5%98%C3%ADdic%C3%AD%20mikrokontroler/%C5%98%C3%ADdic%C3%AD%20mikrokontrol%C3%A9r%20PCB.svg" width="70%" alt="PCB – Řídicí mikrokontrolér"/>`{=html}`<br/>`{=html}
`<em>`{=html}Řídicí mikrokontrolér`</em>`{=html}
```{=html}
</p>
```
```{=html}
<p align="center">
```
`<img style="border: 2px solid #bbb; border-radius: 6px;" src="PCB/Nap%C3%A1jec%C3%AD%20zdroj/Nap%C3%A1jec%C3%AD%20zdroj%20PCB.svg" width="70%" alt="PCB – Napájecí zdroj"/>`{=html}`<br/>`{=html}
`<em>`{=html}Napájecí zdroj`</em>`{=html}
```{=html}
</p>
```

------------------------------------------------------------------------

## Výsledky měření

Přesnost voltmetru byla ověřena porovnáním se dvěma školními digitálními
multimetry.

  ------------------------------------------------------------------------
       Měřené napětí          Naměřeno   Absolutní chyba   Relativní chyba
              (ref.)        voltmetrem                ΔU                δU
  ------------------ ----------------- ----------------- -----------------
           −24,219 V         −24,492 V          −0,273 V            1,13 %

            −8,342 V          −8,445 V          −0,103 V            1,24 %

             6,677 V           6,834 V          +0,157 V            2,35 %

            12,977 V          12,203 V          +0,227 V            1,89 %

            24,217 V          24,654 V          +0,437 V            1,81 %
  ------------------------------------------------------------------------

Absolutní chyba vykazuje lineární závislost na měřeném napětí:
$\Delta U \approx 0{,}0136 \cdot U_{ref}$

Typická relativní chyba v pracovním rozsahu je **1,1 -- 2,7 %**.

------------------------------------------------------------------------

## Klíčové součástky

  Blok                      Součástky
  ------------------------- ----------------------------------------
  Přístrojový zesilovač     TL071, TL072
  Integrátor + komparátor   TL072, LM311
  Analogové přepínače       CD4051B, CD4052B, CD4053B
  Napěťová reference        TL431ACZ + JFET proudový zdroj (J111)
  Mikrokontrolér            ESP32 DEVKIT
  Displej                   1602 LCD + I²C backpack PCF8574
  Napájení                  LM7815, LM7915, LM7805, L78L08, L79L08

Plný kusovník je součástí [dokumentace
(PDF)](Dlouhodob%C3%A1%20maturitn%C3%AD%20pr%C3%A1ce/DMP_Loskot.pdf).

------------------------------------------------------------------------

**Autor:** Martin Loskot · **Vedoucí:** Ing. Jan Novotný, Ph.D. · **SPŠE
Ječná, Praha 2 · 2026**
