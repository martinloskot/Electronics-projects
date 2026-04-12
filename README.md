# Elektronické projekty – Martin Loskot

Repozitář dokumentuje moje elektronické projekty z doby studia na [SPŠE Ječná](https://www.spsejecna.cz/) (obor Elektrotechnika – Elektronické a počítačové systémy). Najdeš tu schémata, návrhy plošných spojů, výpočty a výsledky měření.

Schémata a PCB jsou navržena v **KiCadu**.

---

## Projekty

### 🔬 [Digitální voltmetr – ADC s dvojí integrací](./voltmetr/)

Dlouhodobá maturitní práce (2026). Stolní digitální voltmetr postavený na principu analogově-digitálního převodníku s dvojí integrací – bez použití integrovaného ADC, čistě na diskrétních součástkách.

<p align="center">
  <img src="voltmetr/fotky/P%C5%99edn%C3%AD%20strana.png" width="70%" alt="Voltmetr – přední strana"/><br/>
  <em>Hotový přístroj</em>
</p>

**Hlavní vlastnosti:**
- Měřicí rozsah ±25 V, rozlišení ~4 platné číslice
- Vstupní přístrojový zesilovač (TL071 + TL072) s vysokou vstupní impedancí (řád TΩ)
- Samočinné nulování (autozero) před každým převodem
- Řízení pomocí ESP32, zobrazení na LCD 1602 přes I²C
- Vlastní síťový napájecí zdroj (±15 V, symetrický)
- 5 samostatných desek plošných spojů navržených v KiCadu

---

### 📡 [Zesilovač ve třídě A – BC547C](./zesilova%C4%8D%20ve%20t%C5%99%C3%ADd%C4%9B%20A/)

Nízkofrekvenční tranzistorový zesilovač pro malé signály pracující ve třídě A se společným emitorem. Projekt zahrnuje kompletní výpočet pracovního bodu, návrh hodnot součástek z řady E12, ověření měřením a návrh PCB.

**Hlavní vlastnosti:**
- Napájení 10 V, klidový proud 6 mA, pracovní bod U_C = 5 V
- Naměřené napěťové zesílení A_u ≈ 11,26
- Stabilizace pracovního bodu emitorovým odporem
- Schéma + PCB v KiCadu, výpočty v Excelu

---

## Nástroje

| Nástroj | Použití |
|---|---|
| [KiCad](https://www.kicad.org/) | Schémata a návrh PCB |
| Microsoft Excel | Výpočty pracovních bodů a zpracování měření |
| ESP32 / Arduino IDE | Firmware voltmetru |

---

**Autor:** Martin Loskot · SPŠE Ječná, Praha · 2026
