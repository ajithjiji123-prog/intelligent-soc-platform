# Evidence and Attribution

## Source

This portfolio version is based on the public repository [alen97mathew-gif/intelligent-soc-platform](https://github.com/alen97mathew-gif/intelligent-soc-platform). The original README identifies Alen as the author and says the documentation was finalized on 6 October 2026. The project was collaborative; the portfolio owner describes their contribution as sharing most of the work. This copy credits Alen and does not claim sole authorship.

## What the source documents

- Three VM roles: Kali test system, Ubuntu monitored endpoint, and Ubuntu SOC monitoring server.
- Wazuh Manager, Indexer, Dashboard, Filebeat, and Agent `003`.
- Suricata EVE JSON integration and Zeek JSON connection-log ingestion.
- Controlled SSH password-guessing test with custom Rule `100100` (level 10).
- FIM test on `/etc/soc-vt-test.txt` with Rule `550`.
- VirusTotal hash lookup with Rule `87103` and a no-record response.
- Rule `533` port-state change evidence associated with reverse-shell-related activity.
- Nmap and Gobuster exercises, with explicit limits on attack-specific evidence.

## What the retained screenshots support

The source README links three genuine screenshots in its `screenshots/` directory:

1. Expanded Rule `533` event detail for Agent `003`, showing a listening-port status change.
2. Threat Hunting view showing Rule `533` at level 7.
3. A populated `wazuh-archives-*` view. Visible records include monitoring-server activity; it does not isolate a Victim-to-Kali shell connection.

They are linked from this portfolio README at the original repository so their source and context remain visible. This staging package does not include copied image files.

## Evidence not retained

The source states that dedicated screenshots for FIM Rule `550`, VirusTotal Rule `87103`, SSH Rule `100100`, Suricata Rule `86601`, Nmap terminal output, and Gobuster terminal output are not in the gallery. The exact custom SSH XML, full configuration exports, exact software versions, Kali IP, and full port inventory are also not retained. No screenshot or configuration has been fabricated for this portfolio package.

## Interpretation limits

- Rule `86601` indicates an integrated Suricata event; inspect its signature before making an attack-specific claim.
- Zeek archive visibility is not equivalent to an alert.
- Rule `550` supports a file-integrity change on the tested path, not malicious intent or universal path coverage.
- Rule `87103` with a no-record message means no reputation record was returned; it does not establish a clean verdict or malware detection.
- Rule `533` supports a port-state change, not a confirmed shell or command-and-control session.
- ATT&CK mappings in the README are behavior mappings for lab exercises, not verified Wazuh coverage metadata.


