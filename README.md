
# LSTM-alapú időjárás-előrejelzés európai fővárosok adataiból

Ez a projekt az Óbudai Egyetem, Mély gépi tanulás tárgyának keretében készült. Célja egy mélytanuláson alapuló modell megvalósítása, amely több európai főváros meteorológiai adataira támaszkodva képes előre jelezni a napi maximális hőmérsékletet.

## Témaválasztás és cél

A projekt célja egy meglévő nyílt meteorológiai adathalmaz felhasználásával egy előrejelző pipeline létrehozása LSTM-alapú modell segítségével. A feladat kiterjed:
- a nyers adat lekérdezésére és feldolgozására,
- időalapú jellemzők előkészítésére több város adatai alapján,
- tanító és validációs készletek létrehozására időablakos szekvenciák formájában,
- egy LSTM modell tanítására és optimalizálására,
- a modell értékelésére és vizualizálására.

## Adatforrás

- Az adatok a [Meteostat](https://dev.meteostat.net/) nyilvános API-ján keresztül kerültek lekérdezésre.
- Az adatok napi felbontásúak, az alábbi jellemzőket tartalmazzák:
  - napi átlaghőmérséklet (`tavg`)
  - minimum hőmérséklet (`tmin`)
  - maximum hőmérséklet (`tmax`)
  - csapadék (`prcp`)
  - szélsebesség (`wspd`)

Az adatok csak akkor kerültek felhasználásra, ha a teljes vizsgált időintervallumban (2000–2024) hiánytalanul elérhetők voltak az adott városra és jellemzőre.

## Modell és pipeline

- A megvalósítás LSTM (Long Short-Term Memory) neurális hálózaton alapul.
- A bemeneti adatok több európai főváros több jellemzőjéből épülnek fel, időablakos szekvenciák formájában.
- A célváltozó a `tmax` érték előrejelzése egy kiválasztott városra.

### Modell paraméterei
- `hidden_size`: 16–128
- `batch_size`: 64–4096
- `learning_rate`: 0.0001–0.003
- `num_layers`: 1 vagy 2
- `window_size`: 7 nap

A tanítás során early stopping-et és tanulási görbék mentését használtuk.

## Kiértékelés

A modellek összehasonlítása több metrika alapján történt:
- **Mean Absolute Error (MAE)**
- **Mean Squared Error (MSE)**
- tanulási idő (másodpercben)

A kiértékelés eredményei `.csv` formátumban elérhetők a `training_log.csv` fájlban, valamint az egyes epoch-okra vonatkozó tanulási görbék is naplózva vannak.

## Projektfelépítés

```
oe_deep-ml/
├── logs/                           # Tanulási görbék és metrikák log fájljai
├── models/                         # Betanított modellek (.pt)
├── plots/                          # Tanulási görbék ábrái
├── training_log.csv                # Hyperparaméter-tuning eredményei
├── worldcities.csv                 # Városkoordináták (SimpleMaps)
├── european_capitals_weather.csv   # Egyesített, feldolgozott adat
├── weather_data_train.ipynb        # Adatgyűjtés és előkészítés & Modell tanítás és logolás
├── weather_inference.ipynb         # Modell betöltése és előrejelzés
├── results_analysis.ipynb          # Hyperparaméter-tuning eredményeinek kiértékelése
```

## Főbb tanulságok

- A `batch_size` és `learning_rate` értékek optimalizálása nagy hatással van az eredményre.
- A túl nagy rejtett rétegek túltanuláshoz és gyenge generalizációhoz vezettek.
- A `tmax` célváltozó standardizálása torzított előrejelzést eredményezett, ezért a végső modell már az eredeti skálán tanult.
- A tanulási görbék és korai leállás (early stopping) segítettek a túltanulás elkerülésében.

## Követelmények

- Python 3.10+
- numpy
- pandas
- torch
- matplotlib
- scikit-learn
- meteostat
- geopy

## Licenc

MIT licenc — szabadon felhasználható oktatási és kutatási célra.
