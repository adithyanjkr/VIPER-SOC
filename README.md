VIPER-SOC : Threat Detection, Intelligence & Incident Response 🐍

1. Executive Summary

Project VIPER (Vulnerable IP & Payload Eradication Response) is an automated, dual-layer incident response framework integrated directly with Wazuh SIEM. It bridges real-time threat intelligence feeds with endpoint containment mechanisms—blocking malicious network actors and purging infected files automatically without human intervention.

2. Core Capabilities & Defense Modules

Module 1: Network Defense (AbuseIPDB Integration)

    Monitored Vector: Inbound and outbound IP connections captured by system logs.

    Threat Intelligence: Queries the AbuseIPDB API in real time to fetch IP reputation metrics.

    Trigger Condition: Confidence score exceeds 50%.

    Automated Remediation: Generates a Level 10 Alert on the manager and automatically appends the offending IP to /etc/hosts.deny on the target agent.

Module 2: Endpoint File Defense (VirusTotal Integration)

    Monitored Vector: Real-time File Integrity Monitoring (FIM) tracking file creation or modification.

    Threat Intelligence: Queries the VirusTotal API using the calculated SHA256 file hash.

    Trigger Condition: File flagged as positive/malicious by threat engines.

    Automated Remediation: Generates a Level 12 Alert on the manager and executes a silent deletion (rm -f) of the malicious payload on the endpoint.

3. Operational Workflow

    Step 1 — Detection: Agent captures an event (network connection or new file creation) and sends telemetry to the Wazuh Manager.

    Step 2 — Enrichment: Wazuh Manager routes the IP or SHA256 hash through custom integration hooks to external APIs (AbuseIPDB / VirusTotal).

    Step 3 — Rule Evaluation: Wazuh rules check if the returning score exceeds defined severity thresholds.

    Step 4 — Active Response: Upon rule match, the manager instructs the local agent active-response engine to execute immediate containment (IP ban or file deletion).

4. Key Benefits

    Zero-Touch Containment: Reduces Mean Time to Respond (MTTR) from minutes to milliseconds by removing manual analyst triage steps.

    Dual-Domain Coverage: Secures both the network boundary (incoming/outgoing traffic) and the local host filesystem.

    False Positive Reduction: Utilizes strict confidence thresholds (e.g., AbuseIPDB score > 50%) to ensure benign traffic isn't accidentally disrupted.

5. Prerequisites & Technical Requirements

    SIEM Infrastructure: Active Wazuh Manager and at least one connected Linux Wazuh Agent.

    API Access: Valid API keys for both AbuseIPDB and VirusTotal.

    Supported Operating System: Linux (Debian/Ubuntu or RHEL-based distributions).

Author : Adithyan.V
