
# oe_deep-ml

**Időjárás-előrejelzés európai fővárosok meteorológiai adatai alapján mélytanulás segítségével**

## Tartalomjegyzék

- [Áttekintés](#áttekintés)
- [Adatok](#adatok)
- [Modell](#modell)
- [Használat](#használat)
  - [1. Adatgyűjtés és előkészítés](#1-adatgyűjtés-és-előkészítés)
  - [2. Modell tanítása](#2-modell-tanítása)
  - [3. Modell kiértékelése és vizualizáció](#3-modell-kiértékelése-és-vizualizáció)
  - [4. Inference](#4-inference)
- [Fájlstruktúra](#fájlstruktúra)
- [Követelmények](#követelmények)
- [Licenc](#licenc)

## Áttekintés

Ez a projekt célja, hogy mélytanulási módszerekkel (LSTM) előrejelezze az európai fővárosok napi átlaghőmérsékletét. A modell különböző meteorológiai jellemzők alapján tanul, mint például a minimum, maximum hőmérséklet, csapadék és szélsebesség.

## Adatok

- **Forrás**: [meteostat](https://dev.meteostat.net/)
- **Városok**: Európai fővárosok
- **Időszak**: 2010–2024
- **Jellemzők**:
  - `tavg`: napi átlaghőmérséklet
  - `tmin`: napi minimum hőmérséklet
  - `tmax`: napi maximum hőmérséklet
  - `prcp`: napi csapadék
  - `wspd`: napi átlagos szélsebesség

## Modell

- **Architektúra**: LSTM
- **Hyperparaméterek**:
  - `hidden_size`: 16, 32, 64, 128
  - `num_layers`: 1 vagy 2
  - `batch_size`: 64–4096
  - `learning_rate`: 0.0001–0.003
- **Célváltozó**: `tavg` (napi átlaghőmérséklet)

## Használat

### 1. Adatgyűjtés és előkészítés

```bash
pip install -r requirements.txt
```

```python
from met_data import prepare_data
prepare_data()
```

### 2. Modell tanítása

```python
from train import train_model
train_model()
```

### 3. Modell kiértékelése és vizualizáció

```python
from visualize import plot_learning_curves
plot_learning_curves()
```

### 4. Inference

```python
from inference import predict
predict()
```

## Fájlstruktúra

```
oe_deep-ml/
├── data/
│   ├── raw/
│   └── processed/
├── models/
├── logs/
├── notebooks/
│   ├── met_data.ipynb
│   ├── train.ipynb
│   ├── visualize.ipynb
│   └── inference.ipynb
├── scripts/
│   ├── met_data.py
│   ├── train.py
│   ├── visualize.py
│   └── inference.py
├── requirements.txt
└── README.md
```

## Követelmények

- Python 3.10+
- PyTorch
- pandas
- numpy
- matplotlib
- scikit-learn
- meteostat

## Licenc

Ez a projekt az MIT licenc alatt áll. Részletekért lásd a [LICENSE](LICENSE) fájlt.
