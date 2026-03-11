## PhysioNet MIT-BIH Arrhythmia Dataset (from scratch)

![Image](https://archive.physionet.org/physiobank/charts/mitdb.png)

![Image](https://archive.physionet.org/physiobank/charts/slpdb.png)

![Image](https://www.researchgate.net/publication/335038040/figure/fig1/AS%3A789618664435717%401565271168399/Example-of-annotationL-V-in-a-MIT-BIH-arrhythmia-database-record-109-10-sec.jpg)

![Image](https://www.researchgate.net/publication/310898745/figure/fig3/AS%3A961823591387155%401606328022866/The-ECG-signal-in-normal-sinus-rhythm-in-the-MIT-BIH-Arrhythmia-Database.gif)

The **MIT-BIH Arrhythmia Dataset** is one of the **most widely used ECG datasets for arrhythmia detection** in machine learning and deep learning.

It is hosted on **PhysioNet**, a public repository for biomedical signals.

Researchers use this dataset to train models like:

* CNN
* RNN / LSTM
* Transformers
* MLP
* Hybrid models

for **automatic ECG arrhythmia detection**.

This dataset is very relevant to your work because you are studying **arrhythmia detection using ECG signals**.

---

# 1️⃣ What the MIT-BIH Dataset Is

The dataset contains **ECG recordings from real patients** collected in hospitals.

Main characteristics:

| Feature              | Value                           |
| -------------------- | ------------------------------- |
| Number of recordings | **48 ECG records**              |
| Patients             | **47 individuals**              |
| Duration per record  | **30 minutes**                  |
| Sampling frequency   | **360 Hz**                      |
| ECG leads            | **2 leads per recording**       |
| Total heartbeats     | **~110,000 beats**              |
| Annotation           | **Expert cardiologist labeled** |

Each heartbeat is labeled as:

* Normal beat
* Ventricular beat
* Atrial beat
* etc.

---

# 2️⃣ ECG Leads in MIT-BIH

Each record contains **2 ECG channels**.

Usually:

| Channel   | Lead                    |
| --------- | ----------------------- |
| Channel 1 | Modified Lead II (MLII) |
| Channel 2 | V1 / V2 / V4 / V5       |

So the signal looks like:

```
Time →
Lead 1:  ECG waveform
Lead 2:  ECG waveform
```

Example structure:

```
record 100
   ├── lead1 signal
   ├── lead2 signal
   └── annotations
```

---

# 3️⃣ Files Inside the Dataset

Each ECG record has **3 main files**.

Example:

```
100.dat
100.hea
100.atr
```

### 1️⃣ `.dat` — Raw ECG Signal

Contains **binary ECG waveform data**.

Example signal values:

```
[0.12, 0.15, 0.21, 0.18, -0.02, ...]
```

This is the **actual ECG voltage over time**.

---

### 2️⃣ `.hea` — Header File

Contains **metadata**.

Example:

```
100 2 360 650000
100.dat 212 200 11 1024 995 -22131 0 MLII
100.dat 212 200 11 1024 1011 20052 0 V5
```

Meaning:

| Field | Meaning            |
| ----- | ------------------ |
| 2     | number of signals  |
| 360   | sampling frequency |
| MLII  | lead type          |

---

### 3️⃣ `.atr` — Annotation File

Contains **expert labels for heartbeats**.

Example annotation:

```
Time (sample)    Beat type
77               N
370              N
662              V
946              N
```

Meaning:

| Symbol | Meaning                   |
| ------ | ------------------------- |
| N      | Normal beat               |
| V      | Ventricular ectopic beat  |
| A      | Atrial beat               |
| L      | Left bundle branch block  |
| R      | Right bundle branch block |
| /      | Paced beat                |

---

# 4️⃣ How the Data Looks (Important)

The ECG signal is a **time series signal**.

Example:

```
ECG voltage

1.0 |        /\        /\        /\
    |       /  \      /  \      /  \
0.0 |______/    \____/    \____/    \____
    |
    +------------------------------------
        time →
```

Each **peak** = **heartbeat (QRS complex)**.

The annotation file tells **what type of beat it is**.

---

# 5️⃣ How the Data Is Used for Machine Learning

Typical pipeline:

```
Raw ECG signal
      ↓
Beat detection
      ↓
Extract heartbeat segments
      ↓
Label using annotation
      ↓
Train ML/DL model
```

Example:

```
ECG signal
↓
R peak detection
↓
Extract 200 samples around peak
↓
Classification
```

---

# 6️⃣ Heartbeat Segmentation

A single heartbeat looks like:

```
P wave
QRS complex
T wave
```

Example segment:

```
[-0.02, -0.01, 0.10, 0.55, 1.2, 0.6, 0.1, -0.02, ...]
```

Usually we take:

```
90 samples before R peak
90 samples after R peak
```

Total:

```
180 samples per beat
```

So the dataset becomes:

```
number_of_beats × 180 samples
```

Example:

```
110000 × 180
```

---

# 7️⃣ Beat Classes

Common classes used in ML papers:

| Class | Meaning          |
| ----- | ---------------- |
| N     | Normal           |
| S     | Supraventricular |
| V     | Ventricular      |
| F     | Fusion           |
| Q     | Unknown          |

Example label vector:

```
N N N N V N S N N
```

---

# 8️⃣ How Researchers Convert the Data

Final ML dataset looks like:

```
X shape = (beats, samples)

Example:

X = (110000, 180)
y = (110000)
```

For CNN:

```
X = (110000, 180, 1)
```

For RNN:

```
X = (110000, 180, 1)
```

For MLP:

```
X = (110000, 180)
```

---

# 9️⃣ How to Load the Dataset in Python

Install library:

```
pip install wfdb
```

Example code:

```python
import wfdb
import matplotlib.pyplot as plt

# load record
record = wfdb.rdrecord('100', pn_dir='mitdb')

signal = record.p_signal

print(signal.shape)
```

Output:

```
(650000, 2)
```

Meaning:

```
650000 time samples
2 ECG leads
```

---

# 🔟 Load Annotations

```python
annotation = wfdb.rdann('100', 'atr', pn_dir='mitdb')

print(annotation.sample[:10])
print(annotation.symbol[:10])
```

Example output:

```
[77, 370, 662, 946]
['N', 'N', 'V', 'N']
```

---

# 11️⃣ Visualizing ECG Signal

```python
plt.plot(signal[:1000,0])
plt.title("ECG Signal")
plt.show()
```

This shows ECG waveform.

---

# 12️⃣ Handling the Dataset (Full Pipeline)

Real pipeline:

```
Download MIT-BIH
       ↓
Load ECG signals
       ↓
Load annotations
       ↓
Detect R peaks
       ↓
Extract heartbeat segments
       ↓
Label beats
       ↓
Train model
       ↓
Evaluate arrhythmia
```

---

# 13️⃣ Example Final Dataset

Final processed dataset:

```
X shape

(109446, 187)
```

Example heartbeat:

```
[-0.05, -0.04, -0.02, 0.1, 0.6, 1.1, 0.5, 0.1, -0.03 ...]
```

Label:

```
N
```

---

# 14️⃣ Why This Dataset Is Important

It is used for:

* Arrhythmia detection
* ECG classification
* Heartbeat segmentation
* ECG denoising
* ECG feature extraction
* Medical AI research

Most ECG deep learning papers use **MIT-BIH**.

---

# 15️⃣ Challenges in the Dataset

### 1️⃣ Class imbalance

Example:

```
Normal beats = 90%
Arrhythmia = 10%
```

Solution:

```
SMOTE
Data augmentation
Class weighting
```

---

### 2️⃣ Noise

ECG may contain:

* muscle noise
* baseline drift
* electrode noise

---

### 3️⃣ Patient variability

Each patient ECG differs.

---

# 16️⃣ Typical Deep Learning Input

For CNN:

```
Input shape

(batch_size, 180, 1)
```

Example:

```
(64, 180, 1)
```

---

# 17️⃣ Typical Output

```
Softmax layer

[Normal, Ventricular, Supraventricular]
```

Example output:

```
[0.92, 0.05, 0.03]
```

Meaning:

```
92% Normal
```

---

# 18️⃣ Where to Download

Dataset:

```
https://physionet.org/content/mitdb/1.0.0/
```

---

# 19️⃣ Example Record Structure

```
mitdb/
   100.dat
   100.hea
   100.atr

   101.dat
   101.hea
   101.atr
```

---

# 20️⃣ Typical Deep Learning Research Pipeline

```
MIT-BIH dataset
        ↓
Signal preprocessing
        ↓
Beat segmentation
        ↓
CNN / RNN training
        ↓
Arrhythmia classification
        ↓
Deployment (mobile / web)
```

This pipeline matches your project:

**"Enhancing Arrhythmia Diagnosis Through ECG Deep Learning Classification"**

---




To use the **MIT-BIH Arrhythmia Database** with an **Multilayer Perceptron**, you must convert the **raw ECG time-series signals** into **fixed-length numeric feature vectors**, because MLP only accepts **tabular vectors**, not raw long signals.

I’ll explain the **complete pipeline from raw MIT-BIH data → MLP-ready dataset**.

---

# 1️⃣ Understand the Raw Dataset Structure

Each record in the dataset contains:

```
100.dat   → ECG signal
100.hea   → metadata
100.atr   → heartbeat annotations
```

Example ECG signal shape after loading:

```
signal.shape = (650000, 2)
```

Meaning

| Dimension | Meaning      |
| --------- | ------------ |
| 650000    | time samples |
| 2         | ECG leads    |

Sampling rate:

```
360 samples / second
```

So **30 minutes ECG → ~650k samples**.

---

# 2️⃣ Why Raw Data Cannot Go Directly to MLP

MLP requires:

```
X shape = (samples, features)
```

Example:

```
(10000 patients, 20 features)
```

But ECG looks like:

```
(650000 time samples)
```

So we must convert ECG signals into **heartbeat feature vectors**.

---

# 3️⃣ Complete Conversion Pipeline

Raw ECG → MLP dataset pipeline:

```
ECG signal
     ↓
R-peak detection
     ↓
Heartbeat segmentation
     ↓
Normalize heartbeat
     ↓
Flatten heartbeat vector
     ↓
MLP training dataset
```

---

# 4️⃣ Step 1 — Load ECG Signals

Install library:

```
pip install wfdb
```

Python:

```python
import wfdb

record = wfdb.rdrecord("100", pn_dir="mitdb")
signal = record.p_signal
```

Output:

```
(650000, 2)
```

Use one lead for simplicity:

```python
ecg = signal[:,0]
```

---

# 5️⃣ Step 2 — Load Heartbeat Annotations

Annotations tell **where each beat occurs**.

```python
annotation = wfdb.rdann("100", "atr", pn_dir="mitdb")

r_peaks = annotation.sample
labels = annotation.symbol
```

Example:

```
r_peaks = [77, 370, 662, 946]
labels = ['N', 'N', 'V', 'N']
```

Meaning:

```
sample 77 → Normal beat
sample 662 → Ventricular beat
```

---

# 6️⃣ Step 3 — Extract Heartbeat Segments

Around each R-peak extract a window.

Typical research standard:

```
90 samples before R peak
90 samples after R peak
```

Total:

```
180 samples per heartbeat
```

Python:

```python
import numpy as np

beats = []
beat_labels = []

window = 90

for r, label in zip(r_peaks, labels):

    start = r - window
    end = r + window
    
    if start >= 0 and end < len(ecg):
        beat = ecg[start:end]
        
        beats.append(beat)
        beat_labels.append(label)
```

Now:

```
beats shape ≈ (110000, 180)
```

---

# 7️⃣ Step 4 — Convert Labels to Classes

Typical simplified classes:

| Symbol | Class       |
| ------ | ----------- |
| N      | Normal      |
| V      | Ventricular |
| A      | Atrial      |
| L      | LBBB        |
| R      | RBBB        |

Example mapping:

```python
label_map = {
    'N':0,
    'V':1,
    'A':2,
    'L':3,
    'R':4
}

y = [label_map.get(l,0) for l in beat_labels]
```

---

# 8️⃣ Step 5 — Normalize Features

ECG amplitude varies per patient.

Normalize:

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X = scaler.fit_transform(beats)
```

Now:

```
X shape = (110000, 180)
y shape = (110000,)
```

Perfect for MLP.

---

# 9️⃣ Final Dataset for MLP

Example:

| sample | feature1 | feature2 | ... | feature180 | label |
| ------ | -------- | -------- | --- | ---------- | ----- |
| beat1  | -0.04    | -0.02    | ... | 0.01       | N     |
| beat2  | -0.05    | -0.01    | ... | 0.02       | V     |
| beat3  | -0.03    | -0.02    | ... | 0.01       | N     |

Shape:

```
X = (110000, 180)
y = (110000,)
```

---

# 🔟 Train MLP

Example:

```python
from sklearn.model_selection import train_test_split
from sklearn.neural_network import MLPClassifier

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

model = MLPClassifier(
    hidden_layer_sizes=(128,64),
    activation='relu',
    max_iter=300
)

model.fit(X_train, y_train)
```

---

# 11️⃣ Prediction

```python
from sklearn.metrics import classification_report

pred = model.predict(X_test)

print(classification_report(y_test, pred))
```

---

# 12️⃣ MLP Input Visualization

Each heartbeat becomes a vector:

```
[ -0.02, -0.01, 0.03, 0.12, 0.55, 1.2, 0.6, 0.1, ... ]
```

Length:

```
180 features
```

MLP sees it like:

```
Input layer = 180 neurons
Hidden layer = 128
Hidden layer = 64
Output layer = arrhythmia classes
```

---

# 13️⃣ Real Research Improvement

Better features for MLP:

Instead of raw waveform:

```
RR interval
QRS width
P wave amplitude
T wave amplitude
Heart rate
Frequency features
Wavelet features
```

Then dataset becomes:

```
X = (beats, ~30 engineered features)
```

---

# 14️⃣ Final Pipeline

Complete pipeline:

```
MIT-BIH ECG
     ↓
Load signals
     ↓
Load annotations
     ↓
Extract heartbeats
     ↓
Normalize signals
     ↓
Convert labels
     ↓
Create dataset (X,y)
     ↓
Train MLP
```

---

✅ **Final MLP dataset format**

```
X shape = (num_beats, 180)
y shape = (num_beats,)
```

---

💡 Since you are working on **arrhythmia diagnosis**, the **best architecture is actually CNN**, because CNN captures **ECG waveform morphology** better than MLP.
























To make the **MIT-BIH Arrhythmia Database** compatible with a **Convolutional Neural Network**, we must convert the **raw ECG recordings** into **fixed-size heartbeat segments** arranged like tensors.

CNNs work well because ECG is a **signal waveform**, and convolution can detect patterns like **QRS complexes, P waves, and T waves**.

Below is the **complete pipeline from raw MIT-BIH ECG → CNN-ready dataset**.

---

# 1️⃣ Understand Raw MIT-BIH ECG Data

Each record contains:

```
100.dat   → ECG waveform
100.hea   → metadata
100.atr   → beat annotations
```

Typical signal shape after loading:

```
(650000, 2)
```

Meaning:

| Dimension | Meaning      |
| --------- | ------------ |
| 650000    | time samples |
| 2         | ECG leads    |

Sampling rate:

```
360 samples/second
```

Recording duration:

```
~30 minutes
```

CNN cannot directly process this **very long signal**, so we convert it into **short heartbeat segments**.

---

# 2️⃣ CNN Input Format

CNN expects a **tensor**:

For **1D CNN (best for ECG)**

```
(batch_size, signal_length, channels)
```

Example:

```
(100000, 180, 1)
```

Meaning:

| Dimension | Meaning               |
| --------- | --------------------- |
| 100000    | number of beats       |
| 180       | samples per heartbeat |
| 1         | ECG lead              |

---

# 3️⃣ Complete Conversion Pipeline

```
Raw ECG signal
      ↓
Load annotations
      ↓
Find R-peaks
      ↓
Extract heartbeat windows
      ↓
Normalize signals
      ↓
Reshape for CNN
      ↓
Train CNN model
```

---

# 4️⃣ Step 1 — Load ECG Signal

Install library:

```
pip install wfdb
```

Python:

```python
import wfdb

record = wfdb.rdrecord("100", pn_dir="mitdb")
signal = record.p_signal
```

Shape:

```
(650000, 2)
```

Use one lead:

```python
ecg = signal[:,0]
```

---

# 5️⃣ Step 2 — Load Beat Annotations

Annotations mark **R-peak locations and beat types**.

```python
annotation = wfdb.rdann("100", "atr", pn_dir="mitdb")

r_peaks = annotation.sample
labels = annotation.symbol
```

Example:

```
r_peaks = [77, 370, 662, 946]
labels  = ['N','N','V','N']
```

Meaning:

| Sample | Beat        |
| ------ | ----------- |
| 77     | Normal      |
| 662    | Ventricular |

---

# 6️⃣ Step 3 — Extract Heartbeat Segments

CNN works best with **individual heartbeat windows**.

Typical segmentation:

```
90 samples before R peak
90 samples after R peak
```

Total:

```
180 samples
```

Python:

```python
import numpy as np

window = 90

beats = []
beat_labels = []

for r, label in zip(r_peaks, labels):

    start = r - window
    end = r + window
    
    if start >= 0 and end < len(ecg):

        beat = ecg[start:end]

        beats.append(beat)
        beat_labels.append(label)

beats = np.array(beats)
```

Shape:

```
(110000, 180)
```

---

# 7️⃣ Step 4 — Normalize Signals

Normalize ECG amplitude.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

beats = scaler.fit_transform(beats)
```

---

# 8️⃣ Step 5 — Convert Labels

Example mapping:

```python
label_map = {
    'N':0,
    'V':1,
    'A':2,
    'L':3,
    'R':4
}

y = [label_map.get(l,0) for l in beat_labels]
```

Convert to numpy:

```python
y = np.array(y)
```

---

# 9️⃣ Step 6 — Reshape for CNN

CNN expects **channels dimension**.

```python
X = beats.reshape(-1, 180, 1)
```

Final dataset:

```
X shape = (110000, 180, 1)
y shape = (110000,)
```

---

# 🔟 Train/Test Split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

---

# 11️⃣ CNN Model Example

Example **1D CNN architecture**:

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Conv1D, MaxPooling1D
from tensorflow.keras.layers import Flatten, Dense

model = Sequential([

    Conv1D(32, kernel_size=5, activation='relu', input_shape=(180,1)),
    MaxPooling1D(2),

    Conv1D(64, kernel_size=5, activation='relu'),
    MaxPooling1D(2),

    Flatten(),

    Dense(64, activation='relu'),
    Dense(5, activation='softmax')
])

model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)
```

---

# 12️⃣ Train CNN

```python
model.fit(
    X_train,
    y_train,
    epochs=20,
    batch_size=64,
    validation_data=(X_test, y_test)
)
```

---

# 13️⃣ CNN Input Visualization

Each input sample looks like:

```
[-0.02, -0.01, 0.05, 0.2, 0.9, 1.3, 0.7, 0.2, -0.03 ...]
```

CNN scans this signal using **convolution filters**.

Example learned patterns:

| Filter  | Detects         |
| ------- | --------------- |
| filter1 | QRS complex     |
| filter2 | P wave          |
| filter3 | T wave          |
| filter4 | abnormal spikes |

---

# 14️⃣ Final CNN Dataset Structure

| Item | Shape            |
| ---- | ---------------- |
| X    | (110000, 180, 1) |
| y    | (110000,)        |

Example batch:

```
(64, 180, 1)
```

---

# 15️⃣ Why CNN Works Better Than MLP for ECG

| Feature                        | MLP | CNN |
| ------------------------------ | --- | --- |
| Uses waveform structure        | ❌   | ✅   |
| Detects local ECG patterns     | ❌   | ✅   |
| QRS detection                  | ❌   | ✅   |
| State-of-art arrhythmia models | ❌   | ✅   |

Most ECG papers use **1D CNN**.

---

✅ **Final pipeline for CNN**

```
MIT-BIH dataset
      ↓
Load ECG signals
      ↓
Load annotations
      ↓
Extract heartbeat windows
      ↓
Normalize
      ↓
Reshape (beats,180,1)
      ↓
Train CNN
      ↓
Predict arrhythmia
```

---

