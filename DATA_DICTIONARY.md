# Data dictionary

| Column | Meaning | Unit |
|---|---|---|
| timestamp | Time the feature window was logged | ISO-like local timestamp |
| label | Verified condition label assigned by operator | text |
| rms | RMS of centred ADC counts | ADC counts |
| peak_to_peak | Maximum minus minimum ADC reading in window | ADC counts |
| zero_crossing_rate | Sign changes divided by N-1 | ratio |
| samples | Number of ADC samples in window | samples |

`sample_features.csv` contains synthetic values generated only to test the software workflow. Do not present it as measured experimental data.
