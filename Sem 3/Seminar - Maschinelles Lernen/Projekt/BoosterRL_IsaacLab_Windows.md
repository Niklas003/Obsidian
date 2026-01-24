# Booster RL + Isaac Lab (Windows-only Setup)

## Ziel
Dieses Dokument beschreibt das **vollständig funktionierende Setup** für:
- Training von Booster-Robotern (Fight / Dance / später Walk)
- mit **Isaac Lab**
- auf **Windows**
- mit **RTX 5080**
- **ohne WSL**, **ohne Isaac Gym**
- inkl. **Motion CSV → NPZ Workflow**

Dieses Dokument entspricht dem **aktuellen Stand** der BoosterRobotics-Repos.

---

## 1. Grundentscheidungen (wichtig)

### ❌ Nicht verwendet
- Isaac Gym (Legacy, Python ≤3.8)
- WSL / Linux Dual Boot
- Eigene Python-venvs für Isaac Lab

### ✅ Verwendet
- **Isaac Sim 5.x (Windows)**
- **Isaac Lab**
- **booster_train**
- **booster_assets**
- **Isaac-Sim-Python (`python.bat`)**
- PyTorch CUDA 12.x

> **Merksatz:**  
> *Isaac Sim IST die Python-Umgebung. Alles läuft über `python.bat`.*

---

## 2. Ordnerstruktur

```
C:\Users\<USER>\rl_walk
├── isaac_lab
├── booster_train
├── booster_assets
└── booster_gym        # optional, legacy (nur Referenz)
```

---

## 3. Installation: Isaac Sim (Windows)

### 3.1 Omniverse Launcher
1. NVIDIA Omniverse Launcher installieren
2. Im Launcher **Isaac Sim 5.x** installieren

Typischer Installationspfad:
```
C:\Users\<USER>\AppData\Local\ov\pkg\isaac-sim
```

### 3.2 Test
```powershell
python.bat -c "import omni; print('omni OK')"
```

---

## 4. Installation: Isaac Lab

Isaac Lab **nicht per pip installieren**.

```powershell
cd C:\Users\<USER>\rl_walk\isaac_lab
isaaclab.bat --install
```

Test:
```powershell
python.bat -c "import isaaclab; print('isaaclab OK')"
```

---

## 5. Zentrale Regel (sehr wichtig)

### ❌ Falsch
```powershell
python train.py
```

### ✅ Richtig
```powershell
python.bat train.py
```

---

## 6. booster_assets installieren

```powershell
cd C:\Users\<USER>\AppData\Local\ov\pkg\isaac-sim
.\python.bat -m pip install -e C:\rl_walk\booster_assets
```

Test:
```powershell
python.bat -c "import booster_assets; print('booster_assets OK')"
```

---

## 7. booster_train installieren

```powershell
.\python.bat -m pip install -e C:\Users\<USER>\rl_walk\booster_train\source\booster_train
```

Test:
```powershell
python.bat -c "import booster_train; print('booster_train OK')"
```

### Achtung ⚠️
Bei diesem smoke test kann es passieren dass der Fehler: 
```python
ModuleNotFoundError: No module named 'omni.physics'
```
auftritt. Das ist normal und soweit in Ordnung solange der Test

```powershell
python.bat -c "import omni; print('omni OK')"
```
Erfolgreich ist denn dann ist das omni Modul erfolgreich installiert. Denn um das `booster_train` Modul zu importieren muss zunächst das `omni` Modul importiert werden. Das passiert bei diesem smoke test jedoch nicht.

---

## 8. Motion-Workflow (WICHTIG)

### 8.1 Problem
- `booster_assets` liefert **CSV**
- `booster_train` erwartet **NPZ**

### 8.2 Lösung (offiziell)
CSV → NPZ konvertieren mit bereitgestelltem Script.

### 8.3 Beispiel: Fight 001 (30 FPS)

```powershell
cd C:\Users\<USER>\AppData\Local\ov\pkg\isaac-sim

python.bat C:\Users\<USER>\rl_walk\booster_train\scripts\csv_to_npz.py ^
  --headless ^
  --input_file C:\rl_walk\booster_assets\motions\K1\k1_fight_001.csv ^
  --input_fps 30 ^
  --output_name C:\rl_walk\booster_assets\motions\K1\k1_fight_001.npz
```

Nachher vorhanden:
```
booster_assets/motions/K1/k1_fight_001.npz
```

---

## 9. Tasks auflisten

```powershell
python.bat C:\Users\<USER>\rl_walk\booster_train\scripts\list_envs.py
```

---

## 10. Training starten (Smoke Test)

```powershell
python.bat C:\Users\<USER>\rl_walk\booster_train\scripts\rsl_rl\train.py --task=Booster-K1-Fight_001-v0 --num_envs=256 --headless --device cuda:0
```

---

## 11.  Training stoppen und Checkpoint path

Das Training kann ganz normal mit `ctrl + c` gestoppt werden

Die Logs/Checkpoints zum Training findet sich im `rl_walk` logs

```
C:\Users\<USER>\rl_walk\isaac_lab\_isaac_sim\logs\rsl_rl
```

Die neueste `.pt` Datei ist unser Checkpoint den wir haben wollen.

---
## 12. Häufige Fehler & Fixes

- `ModuleNotFoundError: omni` → nicht `python.bat` benutzt
- `ModuleNotFoundError: booster_assets` → nicht installiert
- `Invalid file path *.npz` → CSV→NPZ vergessen

---

## 13. Fazit

Dieses Setup ist:
- Windows-only
- RTX-5080-kompatibel
- offiziell vorgesehen
- stabil

Ab hier Fokus auf Training & spätere T1/Walk-Portierung.
