# System Architecture

```mermaid
flowchart TD
    A[Induction Motor] --> B[Microphone / Acoustic Sensor]
    B --> C[ESP32 ADC Sampling]
    C --> D[Feature Extraction: RMS, P2P, ZCR]
    D --> E[USB Serial JSON]
    E --> F[Python Data Logger]
    F --> G[Labelled Feature CSV]
    G --> H[Random Forest Training]
    H --> I[Saved Model]
    I --> J[Python Prediction]
    J --> K[Motor Condition Output]
```

## Interface contract
Example serial message:

```json
{"samples":4000,"rms":42.1234,"peak_to_peak":350,"zero_crossing_rate":0.102000}
```

The numeric values above are illustrative only.
