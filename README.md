flowchart TB

    A[Binary Codes]:::main

    %% First Level: Core Families
    PB[Pure Binary Codes<br>Examples: Natural Binary, Straight Binary]
    WC[Weighted Codes<br>Examples: BCD 8421, 2421, Excess-3, 5211]
    NWC[Non-Weighted Codes<br>Examples: Gray Code, Johnson Code, Fibonacci Code]

    %% Second Level: Specialized Codes
    ALPHA[Alphanumeric Codes<br>Examples: ASCII, Extended ASCII, Unicode]
    EDC[Error-Detecting Codes<br>Examples: Parity (even/odd), VRC, LRC]
    ECC[Error-Detecting & Correcting Codes<br>Examples: Hamming Code, CRC, Reed–Solomon]

    %% Third Level: Signed and Special Codes
    SNR[Signed Number Representations<br>Examples: Sign-Magnitude, 1's Complement, 2's Complement, Excess-128]
    SDC[Special Digital Logic Codes<br>Examples: Gray (again), Biquinary, Ring Counter Codes]

    %% Connections
    A --> PB
    A --> WC
    A --> NWC

    PB --> ALPHA
    WC --> EDC
    NWC --> ECC

    A --> SNR
    SNR --> SDC

    %% Styles
    classDef main fill:#fef7e0,stroke:#333,stroke-width:2px,font-weight:bold;
    class PB,WC,NWC,ALPHA,EDC,ECC,SNR,SDC fill:#e0f7fa,stroke:#333,stroke-width:1.5px;