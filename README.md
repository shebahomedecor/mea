# MEA – Modbus Exposure Analyzer

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/Status-Beta-blue)

**MEA provides critical visibility into exposed Modbus devices by analyzing behavioral patterns and infrastructure context, empowering security teams to identify vulnerabilities and risks in ICS/OT environments.**

---

## Why This Project Matters

The proliferation of internet-connected Industrial Control Systems (ICS) and Operational Technology (OT) introduces significant cybersecurity risks. Modbus TCP, a widely used industrial protocol, is frequently exposed online, creating an attractive target for adversaries. Traditional network scanning often fails to distinguish between legitimate devices, simulators, or honeypots, and lacks behavioral context.

MEA addresses this gap by offering a specialized analysis framework. It goes beyond basic connectivity checks to infer device behavior, assess real-world exposure, and provide actionable risk intelligence for security professionals tasked with protecting critical infrastructure.

---

## Key Features

-   **Modbus TCP Connectivity:** Robust connection and data acquisition on port 502.
-   **Passive Register Analysis:** Collects multiple register snapshots over time with rate limiting.
-   **Behavioral Anomaly Detection:** Identifies abnormal patterns and changes in register values.
-   **Entropy & Change Rate Analysis:** Quantifies randomness and volatility of device data.
-   **Simulator / Honeypot Detection:** Pinpoints devices exhibiting fixed datasets or predictable behavior.
-   **Public Exposure Assessment:** Determines if a device is publicly exposed vs. internal network.
-   **IP Infrastructure Context:** Leverages WHOIS lookups for IP ownership (ISP/datacenter).
-   **Risk Scoring Engine:** Consolidates analysis results into a clear, prioritized risk score.
-   **Flexible Reporting:** Generates human-readable console output, detailed JSON, and Markdown reports.

---

## How It Works

MEA employs a multi-faceted approach to analyze Modbus device characteristics:

1.  **Connect & Collect:** Establishes a Modbus TCP connection and passively collects multiple snapshots of register values over a configurable period.
2.  **Analyze Behavioral Patterns:**
    *   **Entropy:** Quantifies the randomness of collected register values to identify static or highly predictable datasets, common in simulators or honeypots.
    *   **Change Rate:** Monitors how register values evolve over time, detecting devices that are truly dynamic versus those with static or infrequent updates.
3.  **Assess Network Exposure:** Performs IP ownership (WHOIS) lookups to determine if the device's IP belongs to a public cloud provider, datacenter, or known internal network range.
4.  **Integrate Context:** Combines behavioral data with network context to build a comprehensive understanding of the device's operational posture.
5.  **Calculate Risk:** Uses a proprietary scoring engine to aggregate all analysis points into a single, actionable risk level, indicating potential vulnerabilities or misconfigurations.

---

## Installation

Clone the repository and install the required Python packages:

```bash
git clone https://github.com/404saint/mea.git
cd mea
pip install -r requirements.txt
```

---

## Usage

Run the interactive analyzer from the project root:

```bash
python3 mea.py
```

When prompted, enter the target Modbus device's IP address.

To gracefully exit the interactive session:

```bash
ctrl+c
```

Upon completion, detailed reports will be generated in the project directory:

-   `report.json`
-   `report.md`

---

## Example Output

```text
Device classified as: Possible Simulator or Fixed Dataset
Confidence: Medium
Exposure: Public (Datacenter)
Risk Level: High
```

---

## Use Cases

-   **Internet-wide Scanning:** Identify publicly exposed Modbus services and assess their inherent risk.
-   **Honeypot/Simulator Detection:** Distinguish between live ICS assets and deceptive emulations.
-   **Penetration Testing:** Validate ICS exposure, identify misconfigurations, and assess the behavioral integrity of target devices.
-   **Security Monitoring:** Augment OT security posture by providing passive behavioral insights into Modbus assets.

---

## Project Structure

```text
.
├── core/             # Handles Modbus connection and data collection
├── analysis/         # Implements entropy and behavioral analysis logic
├── network/          # Manages IP context and exposure assessment (WHOIS)
├── risk/             # Contains the risk scoring and evaluation engine
├── reporting/        # Generates console, JSON, and Markdown output
├── utils/            # Utility functions (e.g., logging, helpers)
├── mea.py            # Main application entry point
├── requirements.txt  # Python dependencies
└── README.md         # Project documentation
```

---

## Roadmap (v2 – Coming Soon)

Planned enhancements for future versions include:

-   **MAC Address Discovery:** Integrate local network device identification for deeper context.
-   **Device Fingerprinting:** Implement vendor and model guessing based on Modbus data patterns.
-   **Passive Function Analysis:** Analyze common Modbus function codes for further behavioral insights.
-   **Continuous Monitoring Mode:** Enable long-term observation and trend analysis for critical assets.
-   **Anomaly Detection Alerts:** Implement real-time alerting for significant behavioral shifts.
-   **ICS Asset Inventory:** Develop capabilities to build and maintain an inventory of Modbus devices.

---

## Security Notice

This tool is designed for **authorized security testing, research, and educational purposes only**.

**Never scan or interact with systems without explicit, prior permission from the asset owner.** Misuse of this tool may lead to legal consequences or disruption of critical operations. The author is not responsible for any unauthorized or malicious use.

---

## Contributing

Contributions are welcome! Please feel free to open issues for bugs or feature requests, or submit pull requests with improvements.

---

## Author

**[Your Name/Alias]** – Security researcher with a focus on practical ICS/OT cybersecurity analysis and defensive strategies.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.