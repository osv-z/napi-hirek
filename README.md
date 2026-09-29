# Napi hírek

Minden reggel letölti a hazai és nemzetközi hírportálok RSS-csatornáit, az azonos eseményről
szóló cikkeket egy hírbe vonja össze, a több forrásban szereplőket előre sorolja, és az
eredményt a `docs/hirek.json` fájlba menti. A GitHub Pages ezt ingyenesen elérhetővé teszi
az app számára. Nincs benne AI, ezért API-kulcsra sincs szükség.

## Beállítás

1. **GitHub-repó:** töltsd fel az összes fájlt (a `.github` mappát is). A repónak nyilvánosnak
   kell lennie, hogy az ingyenes GitHub Pages működjön.
2. **GitHub Pages:** Settings → Pages → Source: „Deploy from a branch”,
   Branch: `main`, mappa: `/docs`.
3. **Első futtatás:** Actions fül → „Napi hírek” → Run workflow.

Az app címe: `https://<felhasznalonev>.github.io/<repo-neve>/`

## Az app telepítése a telefonra

- **Android (Chrome):** nyisd meg a címet, majd koppints a „Telepítés” gombra.
- **iPhone (Safari):** Megosztás gomb → „Főképernyőhöz adás”.

Ha módosítod az appot, a `docs/sw.js` elején növeld a `VERZIO` számát.

## Helyi tesztelés

```bash
pip install -r requirements.txt
python hirosszefoglalo.py
cd docs && python -m http.server 8000   # majd: http://localhost:8000
```

## Testreszabás

- Források: `HAZAI_FORRASOK` és `NEMZETKOZI_FORRASOK` a szkript elején.
  Ha egy forrás 0 cikket ad, valószínűleg megváltozott az RSS-címe.
- Hírek száma: `HAZAI_DB`, `NEMZETKOZI_DB`.
- Csoportosítás érzékenysége: `HASONLOSAG` (kisebb érték = több cikket von össze).

## Megjegyzések

- A csoportosítás a címek szavai alapján működik, ezért ha két forrás nagyon eltérő
  szavakkal írja le ugyanazt az eseményt, külön hírként jelenhet meg.
- A nemzetközi hírek a forrásoldalak nyelvén (angolul) jelennek meg.
- A GitHub ütemezett futásai néha 10-30 percet késnek.
- 
