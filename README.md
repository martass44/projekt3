Pro spuštění skriptu je vhodné vytvořit nové virtuální prostředí a aktivovat ho:

bash
Zkopírovat
Upravit
python -m venv venv
Na Linuxu/macOS aktivujete prostředí pomocí:

bash
Zkopírovat
Upravit
source venv/bin/activate
Na Windows:

cmd
Zkopírovat
Upravit
venv\Scripts\activate
Potřebné knihovny je možné nainstalovat v tomto prostředí pomocí přiloženého souboru requirements.txt:

bash
Zkopírovat
Upravit
pip install -r requirements.txt
Popis skriptu
Skript main.py slouží ke stažení statistik z voleb ze stránek ČSÚ na této adrese:

https://volby.cz/pls/ps2017nss/ps3?xjazyk=CZ

Funguje tak, že se v terminálu spouští jako skript se dvěma argumenty:

URL odkaz (ohraničený uvozovkami) na územní celek, pro který se mají statistiky stahovat.
Tento odkaz se získá kliknutím ve sloupci "Výběr obce" na výše uvedené stránce.

Například pro okres Kladno:
https://www.volby.cz/pls/ps2017nss/ps32?xjazyk=CZ&xkraj=2&xnumnuts=2102

Název CSV souboru (bez přípony), do kterého se mají statistiky ukládat, např. statistiky_kladno.

Ukázka spuštění:
bash
Zkopírovat
Upravit
python3 main.py 'https://www.volby.cz/pls/ps2017nss/ps32?xjazyk=CZ&xkraj=2&xnumnuts=2102' statistiky_kladno
Co skript dělá
Prochází seznam obcí v daném okrese.

Pro každou obec stáhne výsledky voleb jednotlivých stran.

Výsledky ukládá do CSV souboru ve formátu Unicode UTF-8.

CSV soubor obsahuje jeden řádek pro každou obec. Sloupce reprezentují jednotlivé strany a jejich volební výsledky (počet hlasů, procenta apod.).

Chování při chybách
Při úspěšném spuštění:
Skript vypíše např.:
Začínám stahovat data z https://... a ukládám do souboru statistik_kladno.csv
a poté: Program dokončil stahování.

Při neexistující nebo nereagující URL:
Např.
Error: HTTPSConnectionPool(host='voby.cz', port=443)...
→ Chyba při zadání: První argument není funkční URL nebo stránka nereaguje.

Při špatně zadaném názvu CSV souboru (např. kladno.csv):
→ Chyba při zadání: Neplatný název souboru.
Povolené jsou pouze alfanumerické znaky, podtržítko a pomlčka. Název nesmí obsahovat příponu .csv.

Při funkční URL, ale nesprávné adrese (např. odkaz na celostátní přehled místo konkrétního okresu):
Skript se spustí bez chyby, ale výsledná tabulka CSV neobsahuje relevantní volební data.

