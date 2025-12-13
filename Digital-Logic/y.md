flowchart TB
```
    %% Top-level node
    A[Binary Codes]:::main

    %% Level 1: Core Categories
    PB[**Pure Binary Codes**\nExamples: 1010, 1101]
    WC[**Weighted Codes**\nExamples: BCD 8421, 5211, Excess-3]
    NWC[**Non-Weighted Codes**\nExamples: Gray Code, Johnson Code]

    %% Level 2: Applications / Derived Codes
    ALPHA[**Alphanumeric Codes**\nExamples: ASCII 'A' = 01000001, Unicode '世' = 4E16]
    EDC[**Error-Detecting Codes**\nExamples: Parity Bits, 1010 → 10101]
    ECC[**Error-Correcting Codes**\nExamples: Hamming 7,4 → 0110011]

    %% Level 3: Signed & Special Codes
    SNR[**Signed Number Representations**\nExamples: 2's complement 8-bit: -22 → 11101010]
    SDC[**Special Digital Logic Codes**\nExamples: Gray sequences, Biquinary, Ring Counter]

    %% Connections
    A --> PB
    A --> WC
    A --> NWC

    PB --> ALPHA
    WC --> EDC
    NWC --> ECC

    A --> SNR
    SNR --> SDC

    %% Styling
    classDef main fill:#f2f2f2,stroke:#333,stroke-width:2px;
```