# Technical Design Document

## 1. Objective
Develop a low-cost academic prototype that explores acoustic condition monitoring of an induction motor using an ESP32 and a machine-learning classifier.

## 2. Functional blocks
1. Acoustic sensing: microphone converts sound pressure changes into an analog electrical signal.
2. Acquisition: ESP32 ADC samples the sensor output.
3. Feature extraction: firmware calculates RMS amplitude, peak-to-peak amplitude, and zero-crossing rate for each one-second window.
4. Communication: ESP32 transmits a JSON record over USB serial.
5. Dataset generation: Python logger adds a condition label and stores each window in CSV format.
6. Classification: Python trains a Random Forest using labelled features and predicts a condition class.

## 3. Feature definitions
For centred samples x[n], n = 1...N:

- Mean: μ = (1/N) Σ x[n]
- RMS about the mean: RMS = sqrt((1/N) Σ (x[n] - μ)²)
- Peak-to-peak: P2P = max(raw[n]) - min(raw[n])
- Zero-crossing rate: ZCR = crossings / (N - 1)

These features are simple indicators, not unique signatures of a particular fault. Motor speed, load, microphone position, room acoustics, and sensor gain can all change them.

## 4. Data flow
See the block diagram in `ARCHITECTURE.md`. Each serial JSON line contains:
- `samples`
- `rms`
- `peak_to_peak`
- `zero_crossing_rate`

The logger appends:
- `timestamp`
- `label`

## 5. Model
A Random Forest classifier is used as a baseline because it can model nonlinear boundaries and requires little feature scaling. The training script prints a classification report and confusion matrix. A random row split is only a quick software demonstration; final evaluation should split by independent recording sessions/motor runs to reduce data leakage.

## 6. Validation plan
- Verify sensor wiring and ADC voltage range.
- Capture repeated normal-operation recordings at fixed speed, load, distance, and orientation.
- Collect verified fault-condition recordings only using an instructor-approved guarded rig or reliable labelled datasets.
- Repeat recordings on different sessions.
- Compare per-class precision, recall, F1-score, and confusion matrix.
- Test on a motor/run not used during training.
- Record limitations and false alarms.

## 7. Safety and limitations
This is an educational prototype, not a certified protection relay or industrial diagnostic product. Never create faults by damaging a motor or operating unsafe equipment. Keep clear of rotating parts and exposed electrical conductors. Use supervision and a guarded test arrangement.
