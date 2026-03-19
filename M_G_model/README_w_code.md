```python
import os
import numpy as np
import cv2
import h5py

from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Flatten, Dense

# ==============================
# 🔧 ALL MODEL FILES
# ==============================
MODEL_FILES = {
    "model_weights_2classes.h5": 2,
    "model_weights_4classes.h5": 4,
    "model_weights_5classes.h5": 5,
    "model_weights_9classes.h5": 9,
}

# ==============================
# 🖼 AUTO IMAGE FINDER
# ==============================
def find_image():
    for file in os.listdir():
        if file.lower().endswith((".png", ".jpg", ".jpeg")):
            print(f"✅ Using image: {file}")
            return file
    raise FileNotFoundError("❌ No image found!")

# ==============================
# 🖼 IMAGE PREPROCESS
# ==============================
def preprocess_image(path):
    img = cv2.imread(path)

    if img is None:
        raise ValueError(f"❌ Cannot read image: {path}")

    img = cv2.resize(img, (48,48))
    img = img / 255.0
    img = np.expand_dims(img, axis=0)

    return img

# ==============================
# 🧠 UNIVERSAL MODEL BUILDER
# ==============================
from tensorflow.keras.layers import Conv2D, MaxPooling2D

def build_model(num_classes):
    if num_classes == 9:
        model = Sequential([
            Conv2D(32, (3,3), activation='relu', input_shape=(48,48,3)),
            MaxPooling2D(2,2),

            Conv2D(32, (3,3), activation='relu'),
            MaxPooling2D(2,2),

            Flatten(),   # 👉 now becomes 10×10×32 = 3200 ✅
            Dense(128, activation='relu'),
            Dense(9, activation='softmax')
        ])
    else:
        model = Sequential([
            Flatten(input_shape=(48,48,3)),
            Dense(256, activation='relu'),
            Dense(128, activation='relu'),
            Dense(num_classes, activation='softmax')
        ])

    return model

# ==============================
# 🔄 LOAD + FIX MODEL
# ==============================
def load_model_safe(weights_path, num_classes):
    print(f"\n🚀 Processing: {weights_path}")

    try:
        model = build_model(num_classes)
        model.load_weights(weights_path)

        print("✅ Loaded successfully!")
        model.summary()

        return model

    except Exception as e:
        print("❌ Failed:", e)
        return None

# ==============================
# 🎯 MAIN
# ==============================
def main():
    image_path = find_image()
    img = preprocess_image(image_path)

    for weights_file, num_classes in MODEL_FILES.items():

        if not os.path.exists(weights_file):
            print(f"⚠️ Skipping missing file: {weights_file}")
            continue

        model = load_model_safe(weights_file, num_classes)

        if model is None:
            continue

        # 🔍 Prediction
        pred = model.predict(img)
        class_id = np.argmax(pred)
        confidence = np.max(pred)

        print("\n===== RESULT =====")
        print(f"Model: {weights_file}")
        print(f"Prediction: Class {class_id}")
        print(f"Confidence: {confidence:.4f}")
        print("==================")

        # 💾 Save fixed model
        save_name = weights_file.replace(".h5", "_fixed.h5")
        model.save(save_name)
        print(f"💾 Saved: {save_name}")

if __name__ == "__main__":
    main()

```