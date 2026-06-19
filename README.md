# Tennis Biomechanics Classification Model

## Overview
This repository contains a deep learning pipeline and Multilayer Perceptron (MLP) engine designed to classify 10 distinct tennis movements. By analyzing raw 6-axis telemetry data, the model accurately differentiates between right and left-handed serves, forehands, single/double-handed backhands, and overhead strokes, while also extracting swing strength metrics.

## Data Collection Methodology
The baseline dataset for this model was generated using the **Sensor Logger** application:
* [Sensor Logger for iOS](https://apps.apple.com/us/app/sensor-logger/id1531582925)
* [Sensor Logger for Android](https://play.google.com/store/apps/details?id=com.kelvin.sensorapp&hl=en)

During the data collection phase, a smartphone was held directly in the hand as a physical substitute for a tennis racket. This method was utilized to accurately simulate stroke mechanics, measure swing strength, and capture the pure rotational and directional forces of the human arm without external interference. 

## Model Architecture
The system processes the raw `.csv` telemetry into clean, peak-aligned tensors before feeding them into the neural network. 

* **Input:** 640-feature tensor (80-step time window across 8 target variables).
* **Processing:** Features Butterworth low-pass filtering to isolate human movement from static noise.
* **Network:** A deep MLP utilizing Dense layers, Batch Normalization, and aggressive Dropout to prevent overfitting.
* **Optimization:** AdamW optimizer coupled with Cosine Decay Restarts for dynamic learning rate adjustment.

## Hardware Adaptability & Future Scope
While the current model is trained on simulated smartphone telemetry, the architecture is highly adaptable for embedded systems. 

The inference engine can be deployed alongside dedicated hardware sensors (accelerometer, gyroscope, and gravity modules) mounted directly onto a physical tennis racket. 

**Important Note for Hardware Integration:** If transitioning to a physical racket used to hit live tennis balls, the data preprocessing pipeline will require recalibration. You will need to implement additional signal processing (such as adjusting the Butterworth cutoff frequencies or adding impact-masking algorithms) to account for and filter out the severe, high-frequency vibrations caused by the ball striking the racket strings.

## License
This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)**. 

You may copy, distribute, and modify the software as long as you track changes/dates in source files. Any modifications to or software including (via compiler) GPL-licensed code must also be made available under the GPL along with build and install instructions. See the `LICENSE` file for more details.
