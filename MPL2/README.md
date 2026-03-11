To use **MLP (Multilayer Perceptron)** for your project

**“Enhancing Arrhythmia Diagnosis Through ECG Deep Learning Classification Deploying and Augmented Reality 3D Heart Visualization and Interaction”** using the **MIT-BIH Arrhythmia Database**, we need to convert ECG signals into features that an MLP can understand.

I will explain the **complete pipeline simply from scratch**.

---

# 1. Understand the Dataset

The **MIT-BIH Arrhythmia dataset** contains:

* **48 ECG recordings**
* **2 leads per recording**

  * Lead II
  * Modified Lead V1
* **Sampling rate:** 360 Hz
* **Annotations:** Each heartbeat labeled with arrhythmia type.

Example arrhythmia classes:

| Symbol | Meaning                           |
| ------ | --------------------------------- |
| N      | Normal beat                       |
| V      | Premature ventricular contraction |
| A      | Atrial premature beat             |
| L      | Left bundle branch block          |
| R      | Right bundle branch block         |
| F      | Fusion beat                       |

So the ML task is:

**Input → ECG heartbeat signal
Output → Arrhythmia class**

---

# 2. Why Use MLP for ECG

An **MLP works with feature vectors**, not raw signals.

Therefore:

ECG Signal
→ preprocessing
→ feature extraction
→ feature vector
→ MLP classification

---

# 3. Overall System Architecture

```
ECG Signal
     │
     ▼
Signal Preprocessing
     │
     ▼
Heartbeat Segmentation
     │
     ▼
Feature Extraction
     │
     ▼
Feature Vector
     │
     ▼
MLP Classifier
     │
     ▼
Arrhythmia Type
     │
     ▼
Heart Region Mapping
     │
     ▼
3D AR Heart Visualization
```

---

# 4. Step 1 — Load ECG Data

Libraries:

```python
pip install wfdb numpy pandas scikit-learn matplotlib
```

Code:

```python
import wfdb
import numpy as np
import matplotlib.pyplot as plt

record = wfdb.rdrecord('100', pn_dir='mitdb')
annotation = wfdb.rdann('100', 'atr', pn_dir='mitdb')

signal = record.p_signal[:,0]   # Lead II
```

Plot ECG:

```python
plt.plot(signal[:2000])
plt.title("ECG Signal")
plt.show()
```

---

# 5. Step 2 — Heartbeat Segmentation

Each **R-peak represents one heartbeat**.

Using annotation:

```python
r_peaks = annotation.sample
labels = annotation.symbol
```

Extract a window around each beat:

```
200 samples before R peak
200 samples after R peak
```

Code:

```python
beats = []
beat_labels = []

for i in range(len(r_peaks)):
    r = r_peaks[i]

    if r-200 > 0 and r+200 < len(signal):
        beat = signal[r-200:r+200]
        beats.append(beat)
        beat_labels.append(labels[i])

beats = np.array(beats)
```

Each beat becomes:

```
400 ECG samples
```

---

# 6. Step 3 — Feature Extraction

MLP works better with **hand-crafted features**.

Example ECG features:

### Time-domain features

| Feature       | Meaning            |
| ------------- | ------------------ |
| Mean          | signal average     |
| Std           | signal variability |
| Max amplitude | peak height        |
| Min amplitude | trough             |
| RMS           | energy             |

Code:

```python
features = []

for beat in beats:
    f = [
        np.mean(beat),
        np.std(beat),
        np.max(beat),
        np.min(beat),
        np.sqrt(np.mean(beat**2))
    ]
    features.append(f)

X = np.array(features)
```

---

### Frequency features

ECG rhythm info exists in frequency domain.

```python
from scipy.fft import fft

def freq_features(signal):
    f = np.abs(fft(signal))
    return [
        np.mean(f),
        np.std(f),
        np.max(f)
    ]
```

Combine features.

---

# 7. Step 4 — Encode Labels

```python
from sklearn.preprocessing import LabelEncoder

le = LabelEncoder()
y = le.fit_transform(beat_labels)
```

Example mapping:

```
N → 0
V → 1
A → 2
```

---

# 8. Step 5 — Train MLP

```python
from sklearn.model_selection import train_test_split
from sklearn.neural_network import MLPClassifier
from sklearn.preprocessing import StandardScaler
```

Split data:

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

Scale features:

```python
scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)
```

Train MLP:

```python
mlp = MLPClassifier(
    hidden_layer_sizes=(128,64),
    activation='relu',
    solver='adam',
    max_iter=300
)

mlp.fit(X_train, y_train)
```

---

# 9. Step 6 — Evaluate Model

```python
from sklearn.metrics import accuracy_score, classification_report

pred = mlp.predict(X_test)

print("Accuracy:", accuracy_score(y_test, pred))
print(classification_report(y_test, pred))
```

Typical result:

```
Accuracy ≈ 92–96%
```

---

# 10. Step 7 — Save Model

```python
import joblib

joblib.dump(mlp, "arrhythmia_mlp.pkl")
joblib.dump(scaler, "scaler.pkl")
```

---

# 11. Step 8 — Deploy Model (Backend)

You can deploy using **FastAPI**.

Example API:

```python
from fastapi import FastAPI
import joblib
import numpy as np

app = FastAPI()

model = joblib.load("arrhythmia_mlp.pkl")
scaler = joblib.load("scaler.pkl")

@app.post("/predict")
def predict(features:list):

    X = scaler.transform([features])
    pred = model.predict(X)

    return {"arrhythmia": int(pred[0])}
```

---

# 12. Step 9 — Map Arrhythmia to Heart Region

Using ECG lead mapping.

Example:

| Arrhythmia    | Heart Region       |
| ------------- | ------------------ |
| Ventricular   | Ventricles         |
| Atrial        | Atrium             |
| Bundle branch | Conduction pathway |

So the system outputs:

```
Arrhythmia: PVC
Region: Left Ventricle
```

---

# 13. Step 10 — AR 3D Heart Visualization

Pipeline:

```
ML model
     │
     ▼
Prediction (PVC)
     │
     ▼
Region detection
     │
     ▼
Highlight region in 3D heart
```

Technologies:

| Part     | Technology     |
| -------- | -------------- |
| Backend  | FastAPI        |
| ML       | Python + MLP   |
| AR       | Unity + ARCore |
| 3D Heart | Blender model  |

Workflow:

```
Mobile App
     │
     ▼
Upload ECG
     │
     ▼
FastAPI Server
     │
     ▼
MLP Prediction
     │
     ▼
Send arrhythmia + heart region
     │
     ▼
Unity AR app highlights region
```

Example:

```
PVC detected
→ highlight ventricle in red
```

---

# 14. Final System Diagram

```
ECG Signal
     │
     ▼
Signal Preprocessing
     │
     ▼
Beat Segmentation
     │
     ▼
Feature Extraction
     │
     ▼
MLP Classifier
     │
     ▼
Arrhythmia Detection
     │
     ▼
Heart Region Mapping
     │
     ▼
3D AR Heart Visualization
```

---

# 15. Limitations of MLP for ECG

MLP **cannot capture temporal patterns well**.

Better models:

| Model      | Accuracy |
| ---------- | -------- |
| MLP        | ~90–95%  |
| CNN        | ~97%     |
| CNN + LSTM | ~99%     |

MLP is good for **learning basics**.

---
