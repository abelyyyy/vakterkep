# Vaktérkép gyakorló + Érettségi földgömb

Földrajz érettségi topográfia: az Oktatási Hivatal követelményeinek teljes névanyaga (810 név, közép- és emelt szint).

- **`index.html`** – vaktérkép gyakorló: keresés a térképen, névbeírás, tanulás; vizsgaszint-váltó (közép / közép + emelt).
- **`globe.html`** – forgatható földgömb három nézettel:
  - **Atlasz** – letisztult, saját vektoros térkép (határok, partvonal, folyók, tavak, magyar megyék),
  - **Domborzat** – iskolai atlasz-színezés (zöld alföld → barna hegység) és árnyékolás,
  - **Műhold** – Sentinel-2 felhőmentes mozaik.
  - Keresőmező (ékezet nélkül is működik): a választott helyet kijelöli, felcímkézi és odarepül.
  - Fordítva is: a gömbre kattintva kiírja, mi van ott, és felsorolja az ugyanott lévő többi követelmény-elemet is (pl. Bakony → Dunántúli-középhegység → Kárpát-medence …).
  - Kategóriaszűrő névlistával, a vizsgaszint a gyakorlóval közös.
- **`vakterkep-offline.html`** – a gyakorló egyetlen fájlban, internet nélkül is megnyitható (a földgömb nincs benne).

## Közzététel GitHub Pages-en

1. Töltsd fel a mappa teljes tartalmát egy repó gyökerébe (a `tiles/` mappát és a `.nojekyll` fájlt is).
2. A repó **Settings → Pages** oldalán válaszd: *Deploy from a branch* → `main` / `(root)`.
3. Pár perc múlva elérhető: `https://<felhasználónév>.github.io/<repó>/`

A `globe.html` és az `index.html` a JSON-adatokat `fetch`-csel tölti, ezért **webszerverről** kell megnyitni (GitHub Pages, vagy helyben pl. `python3 -m http.server`), nem `file://`-ból.

## Fájlok

| Fájl | Tartalom |
|---|---|
| `base.json` | országhatárok három részletességben, magyar megyék, tavak, folyók (tömörített koordináták) |
| `regions.json` | a 810 követelmény-elem neve, kategóriája, szintje és geometriája |
| `tiles/*.jpg` | helyi alapképek Web Mercator vetületben (domborzat, műhold) – kis nagyításon és akkor látszanak, ha az online csempék nem érhetők el |

A földgömb motorja a [MapLibre GL JS](https://maplibre.org/) 5.24.0 (BSD-3), CDN-ről töltődik.

## Adatforrások és licencek

- Határok, folyók, tavak: [Natural Earth](https://www.naturalearthdata.com/) (közkincs)
- Magyar tájak, nemzeti parkok, egyes tavak és folyók: © [OpenStreetMap](https://www.openstreetmap.org/copyright)-közreműködők (ODbL)
- Magyar megyék: geoHungary; középtájak: a Magyarország kistájainak katasztere alapján
- Kőzetlemezek: Bird (2002) PB2002, [fraxen/tectonicplates](https://github.com/fraxen/tectonicplates)
- Domborzat online: [Mapzen Terrarium / AWS Open Data](https://registry.opendata.aws/terrain-tiles/) (SRTM, GMTED, ETOPO1 stb.)
- Domborzat helyi alapkép: Natural Earth shaded relief + NOAA ETOPO1 (a matplotlib basemap-data csomagból)
- Műhold online: [Sentinel-2 cloudless – s2maps.eu](https://s2maps.eu), EOX IT Services GmbH (Copernicus Sentinel 2020 adatok módosítva) – CC BY-NC-SA 4.0, csak nem kereskedelmi célra
- Műhold helyi alapkép: NASA Blue Marble Next Generation (közkincs)
- Követelmények: Oktatási Hivatal, Földrajz érettségi vizsgakövetelmények – topográfiai fogalmak
