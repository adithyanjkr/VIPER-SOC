<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Project VIPER | Automated Threat Containment</title>
    <style>
        :root {
            --bg-color: #0d1117;
            --card-bg: #161b22;
            --accent-color: #2ea043;
            --accent-alert: #da3633;
            --text-main: #c9d1d9;
            --text-heading: #ffffff;
            --border-color: #30363d;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            line-height: 1.6;
            margin: 0;
            padding: 2rem 1rem;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
        }

        header {
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 1.5rem;
            margin-bottom: 2rem;
            text-align: center;
        }

        h1 {
            color: var(--text-heading);
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
        }

        .subtitle {
            font-size: 1.1rem;
            color: var(--accent-color);
            font-weight: 600;
        }

        .tagline {
            font-style: italic;
            margin-top: 0.5rem;
            color: #8b949e;
        }

        section {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
        }

        h2 {
            color: var(--text-heading);
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 0.5rem;
            margin-top: 0;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 1.5rem;
            margin-top: 1rem;
        }

        .card {
            background: var(--bg-color);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            padding: 1rem;
        }

        .card h3 {
            color: var(--accent-color);
            margin-top: 0;
        }

        .diagram-box {
            background-color: #010409;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            padding: 1rem;
            overflow-x: auto;
            font-family: monospace;
            white-space: pre;
            color: #58a6ff;
            line-height: 1.3;
        }

        ul {
            padding-left: 1.2rem;
        }

        li {
            margin-bottom: 0.5rem;
        }

        .badge {
            background-color: rgba(46, 160, 67, 0.15);
            color: var(--accent-color);
            padding: 0.2rem 0.6rem;
            border-radius: 12px;
            font-size: 0.85rem;
            font-weight: 600;
        }

        footer {
            text-align: center;
            margin-top: 3rem;
            color: #8b949e;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>

    <div class="container">
        
        <header>
            <h1>🐍 Project VIPER</h1>
            <div class="subtitle">Vulnerable IP & Payload Eradication Response</div>
            <div class="tagline">Automated Threat Hunting & Active Containment using Wazuh SIEM, AbuseIPDB, and VirusTotal</div>
        </header>

        <section id="overview">
            <h2>📌 Project Overview</h2>
            <p>
                <strong>Project VIPER</strong> is an automated, dual-layer incident response framework integrated with <strong>Wazuh SIEM</strong>. 
                Designed to operate without analyst intervention, VIPER links real-time threat intelligence feeds directly to agent-side containment mechanisms. 
                When malicious network traffic or suspicious filesystem activity is observed, VIPER evaluates the threat vectors and executes instant remediation to stop lateral movement and payload execution.
            </p>
        </section>

        <section id="architecture">
            <h2>🛡️ Defense Architecture</h2>
            <div class="diagram-box">
                    ┌──────────────────────────────┐
                    │        Wazuh Manager         │
                    └──────────────┬───────────────┘
                                   │
           ┌───────────────────────┴───────────────────────┐
           ▼                                               ▼
[ Network Connection ]                            [ File Event (FIM) ]
           │                                               │
  AbuseIPDB API Check                             VirusTotal API Check
           │                                               │
 Confidence Score > 50%                           Flagged as Malicious
           │                                               │
           ▼                                               ▼
  Rule 100200 (Level 10)                          Rule 100300 (Level 12)
           │                                               │
           ▼                                               ▼
 Block IP (/etc/hosts.deny)                       Delete Payload (rm -f)
            </div>
        </section>

        <section id="modules">
            <h2>⚙️ Core Functional Modules</h2>
            <div class="grid">
                <div class="card">
                    <h3>🌐 Network Defense Module</h3>
                    <ul>
                        <li><strong>Monitored Vector:</strong> Inbound and outbound network connection logs.</li>
                        <li><strong>Threat Intelligence:</strong> Queries <strong>AbuseIPDB API</strong> for IP reputation scoring.</li>
                        <li><strong>Threshold:</strong> Confidence score greater than 50%.</li>
                        <li><strong>Automated Action:</strong> Generates High-Severity Alert and appends offender IP to <code>/etc/hosts.deny</code>.</li>
                    </ul>
                </div>
                <div class="card">
                    <h3>📁 Endpoint File Defense Module</h3>
                    <ul>
                        <li><strong>Monitored Vector:</strong> Real-time File Integrity Monitoring (FIM).</li>
                        <li><strong>Threat Intelligence:</strong> Queries <strong>VirusTotal API</strong> with generated file hash ($SHA256$).</li>
                        <li><strong>Threshold:</strong> Positive malware identification by threat engines.</li>
                        <li><strong>Automated Action:</strong> Generates High-Severity Alert and issues file deletion command (<code>rm -f</code>).</li>
                    </ul>
                </div>
            </div>
        </section>

        <section id="features">
            <h2>🚀 Key Highlights</h2>
            <ul>
                <li><span class="badge">Speed</span> <strong>Zero-Touch Containment:</strong> Drops Mean Time to Respond (MTTR) down to milliseconds.</li>
                <li><span class="badge">Coverage</span> <strong>Dual Domain Protection:</strong> Secures both external network perimeters and local endpoint storage.</li>
                <li><span class="badge">Accuracy</span> <strong>Confidence Thresholds:</strong> Reduces false positives by filtering through reputation engine metrics.</li>
            </ul>
        </section>

        <section id="requirements">
            <h2>🛠️ System Requirements</h2>
            <ul>
                <li><strong>SIEM Platform:</strong> Wazuh Manager & Wazuh Agent</li>
                <li><strong>External APIs:</strong> AbuseIPDB API & VirusTotal API</li>
                <li><strong>Supported Environment:</strong> Linux (Debian / RHEL based)</li>
            </ul>
        </section>

        <footer>
            <p>Project VIPER — Automated SOC Threat Containment Framework</p>
        </footer>

    </div>

</body>
</html>
