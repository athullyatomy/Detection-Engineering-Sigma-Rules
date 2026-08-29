This detection focuses on identifying potential supply chain attacks via malicious npm packages, similar to the Mini Shai‑Hulud campaign (May 2026).


## In such attacks:
A developer installs a compromised package
Malicious scripts execute automatically (preinstall, postinstall)
The script initiates outbound connections to attacker-controlled infrastructure
Credentials (GitHub tokens, API keys, cloud secrets) may be exfiltrated

This rule detects anomalous outbound connections triggered by developer tools (npm/node/code) to suspicious or newly observed domains.

## Detection Logic

Process: npm, node, code, bash
Network connection to:

Unknown / newly observed domains
Suspicious TLDs or domains not previously contacted


## Context:

Triggered during package install phase
Developer workstation activity

## This rule will catch cases where:
A developer installs a package
 npm executes hidden script
Script makes outbound connection to suspicious domain

## Example:
npm install <malicious-package>
   ↓
node.exe → filev2.getsession[.]org

## Future Enhancements

-->Add newly registered domain detection (NRD)
Correlate with:
process_creation events
npm install command-line logs
Add DNS + Proxy + EDR correlation
Detect abnormal GitHub token usage post-execution
