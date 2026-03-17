#Dokumentace 
Projekt: Fotopast
Autor: Jan Vávra
Obor: Informační technologie

##Annotace
Tato práce se zabývá návrhem a realizací nízkonákladové fotopasti založené na mikrokontroleru ESP32-CAM.
Zařízení využívá pasivní infračervené (PIR) čidlo pro detekci pohybu. Po zachycení pohybu systém pořídí
snímek a uloží jej na SD kartu (případně odešle na server). Cílem bylo vytvořit energeticky efektivní a
kompaktní zařízení pro monitorování prostor.

##Úvod
Srdcem projektu je modul ESP32-CAM, který v sobě má rozhraní pro kameru OV2640.
Hlavní výzvou bylo implementovat kod na modul Projekt prochází fázemi od hardwarového
zapojení na nepájivém poli přes programování v prostředí Arduino IDE
až po finální testování v reálných podmínkách.

##Ekonomicka rozvaha:
Běžné fotopasti (značky jako Bunaty, Apeman) začínají na ceně 1 500–3 000 Kč. Jsou uzavřené.
V čem je projekt lepší: Náklady na hardware jsou cca 700 Kč. Projekt je plně modifikovatelný.

##Vývoj
###Vývoj a použité technologie Hardware:
- ESP32-CAM: Hlavní modul s kamerou.
- USB-TTL Převodník: Pro nahrávání kódu (přes piny U0R a U0T).
- PIR Senzor (HC-SR501): Detekce pohybu.
- Nepájivé pole a vodiče: Pro propojení.
###Softwarové členění:
- Program je postaven na platformě Arduino (C++). Kód je rozdělen na:
- Inicializaci: Nastavení kamery a senzorů.
- Režim hlubokého spánku (Deep Sleep): Pro úsporu energie je ESP vypnuté, dokud ho PIR senzor neprobudí přes GPIO pin.
- Obslužnou rutinu: Po probuzení dojde k aktivaci kamery, pořízení snímku a zápisu.

##Testovaní
Scénář,Popis,Očekávaný výsledek,Výsledek
1. Nasazení: Připojení napájení a naběhnutí systému. - "LED blikne, systém čeká na pohyb."
2. Detekce: Pohyb rukou před PIR senzorem. - ESP32 se probudí ze spánku.
3. Pořízení: Snímání za denního světla. - Fotografie je ostrá a čitelná.
4. Ukládání: Kontrola zápisu na SD kartu. - Soubor .jpg je správně uložen.

##Instalace a spuštění
- Zapojení: Propojte ESP32-CAM s USB-TTL převodníkem (5V na 5V, GND na GND, U0R na TX, U0T na RX). Důležité: Pro nahrávání propojte GPIO 0 s GND.
- Software: V Arduino IDE vyberte desku "AI Thinker ESP32-CAM".
- Upload: Nahrajte kód a po dokončení odpojte GPIO 0 od GND a restartujte desku.
- Provoz: Odpojte programátor a připojte baterii nebo jiný zdroj energie.

