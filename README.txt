PÉNZÜGYEIM 2.0 – HELYI DOKUMENTUMMODUL ELŐNÉZET

GitHub Pages telepítés:
1. Csomagold ki ezt a ZIP-et.
2. A benne lévő fájlokat és ikonokat töltsd fel a GitHub repository main ágának gyökerébe, a régiek felülírásával.
3. Várd meg a GitHub Pages frissítését, majd Safari-ban frissítsd az alkalmazást.

Új funkciók:
- Dokumentumok (nyugta, számla, blokk, egyéb bizonylat) rögzítése.
- Kamera/fájl import, helyi IndexedDB dokumentumtárolás.
- Kézi dokumentum- és tételadat-rögzítés.
- HUF dokumentum esetén kiadás automatikus rögzítése a meglévő pénzügyi tételek közé.
- Helyi termékár-előzmény és dokumentumkeresés.

FONTOS KORLÁTOK:
- Ez az első működő adatmodell/UI alapozás, nem kész OCR: a kereskedőt, dátumot, összeget és tételeket jelenleg kézzel kell beírni.
- A dokumentumképek az adott böngésző IndexedDB tárhelyén maradnak. Nem szinkronizálódnak másik eszközre.
- A meglévő pénzügyi JSON-mentés nem tartalmazza a dokumentumképeket és a dokumentumtár IndexedDB rekordjait. A „Dokumentumadatok exportja” csak a strukturált adatokat exportálja, képek nélkül.
- A több pénznemű dokumentumok tárolhatók, de a jelenlegi pénzügyi tranzakciómotor csak HUF könyvelést kezel automatikusan.
- A háztartási munkaterület és a számlák részletfizetése még nincs integrálva.
- Tesztadatokkal próbáld ki; fontos bizonylatokról külön biztonsági másolatot őrizz meg.
