# Test Plan

| Test ID | Test | Expected result |
|---|---|---|
| T01 | Power ESP32 with sensor connected correctly | Board starts and serial port is available |
| T02 | Open serial monitor at 115200 baud | Ready message and JSON feature records appear |
| T03 | Run logger for a short normal-condition session | CSV rows are appended with the selected label |
| T04 | Train using the demonstration CSV | Model file is generated and metrics are printed |
| T05 | Run prediction with numeric features | One predicted class and class probabilities are printed |
| T06 | Repeat collection in another session | New timestamped rows are appended |

## Acceptance notes
Passing these software checks only confirms that the data pipeline runs. It does not prove real fault-detection accuracy. Accuracy claims require real, correctly labelled, representative recordings and independent testing.
