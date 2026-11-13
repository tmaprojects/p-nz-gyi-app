PÉNZÜGYEIM 1.5 – AI BLOKK- ÉS SZÁMLAFELISMERÉS

MI KÉSZÜLT EL?
- A dokumentumfotó automatikusan az AI-felismeréshez kerül, ha beállítottad a saját backend végpontodat.
- A felismerés kinyeri a kereskedőt, helyszínt, bizonylatszámot, dátumot, végösszeget, nettó/ÁFA/kedvezmény adatokat, pénznemet, fizetési módot és a terméktételeket.
- A termékek mennyisége, egysége, ára, kategóriája és visszaváltási díja külön mezőbe kerülhet.
- A felismert adatok a meglévő dokumentuműrlapba töltődnek; mentés előtt ellenőrizhetők és javíthatók.
- Ha nincs AI-végpont beállítva, a meglévő helyi Tesseract OCR marad a tartalék felismerő.
- A dokumentumkép továbbra is az eszköz IndexedDB tárhelyére mentődik. Az AI-feldolgozás idejére a képet elküldi a beállított backendnek és az OpenAI API-nak; a backend store:false beállítást használ.

FONTOS: A GitHub Pages önmagában nem tudja biztonságosan tárolni az OpenAI API-kulcsot. Ezért külön, ingyenes keretű Cloudflare Worker backend szükséges. Az API-használat az OpenAI-nál külön díjas lehet.

BEÁLLÍTÁS – CLOUDFLARE WORKERS
1. Hozz létre egy Cloudflare-fiókot, majd nyisd meg a Workers & Pages részt.
2. Hozz létre egy új Worker projektet.
3. A backend/worker.js teljes tartalmát másold a Worker szerkesztőjébe, majd Deploy.
4. A Worker Settings / Variables and Secrets résznél adj hozzá egy titkos változót:
   Név: OPENAI_API_KEY
   Érték: a saját OpenAI API-kulcsod
   Soha ne tedd ezt a kulcsot a GitHub repositoryba vagy az index.html fájlba.
5. A Worker publikus URL-je például: https://penzugyeim-ai-receipt.<azonosito>.workers.dev
6. Nyisd meg a Pénzügyeim Dokumentumok / Dokumentum scannelése részt.
7. Az „AI-felismerés végpontja” mezőbe illeszd be a Worker URL-jét. A böngésző helyben elmenti.
8. Ezután a fotó kiválasztásakor automatikusan elindul az AI-felismerés. A gombbal újra is futtathatod.

A WORKER KÓD FELTÖLTÉSE
A backend mappában lévő worker.js a Cloudflare Worker teljes forrása. A wrangler.toml fájl a Wrangler CLI-vel történő telepítéshez ad alapbeállítást. A legegyszerűbb módszer a Cloudflare webes Worker szerkesztője.

FRISSÍTÉS A GITHUB PAGES-EN
A ZIP gyökerében található index.html, manifest.json, service-worker.js és ikonok tölthetők fel a meglévő repository gyökerébe, felülírva a régieket. A meglévő pénzügyi localStorage- és dokumentum-IndexedDB-adatkulcsokat nem módosítottam.

ADATVÉDELEM ÉS KORLÁTOK
- Az API-kulcs kizárólag a Worker titkos változója legyen.
- A képet a Worker nem tárolja, csak továbbítja a modellnek; a Responses API kérés store:false beállítást használ.
- A feldolgozáshoz internetkapcsolat kell és API-költség merülhet fel.
- A modell tévedhet, ezért a felismert összeget és terméksorokat mentés előtt ellenőrizd.
- A jelenlegi AI-végpont képfájlokat fogad (PNG/JPG/WEBP); PDF-et előbb képpé kell alakítani.
- A CORS jelenleg minden webes origin felől engedélyezett, de csak a Worker URL-je és az OpenAI kulcs titkossága mellett működik. Éles, többfelhasználós szolgáltatásnál érdemes origin-korlátozást, hitelesítést és használati limitet beállítani.

A FELISMERÉS KÜLSŐ API-T HASZNÁL
Az OpenAI API képes képbemenet értelmezésére és strukturált JSON-válasz előállítására. Dokumentáció: https://developers.openai.com/api/docs/guides/images-vision és https://developers.openai.com/api/docs/guides/structured-outputs
