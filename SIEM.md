# 🛡️ SIEM Lab - Wazuh

This part of my homelab is focused on SIEM monitoring, log collection, alerting, and getting more hands-on with how security events actually look in a live environment.

I’m using Wazuh as the main SIEM/XDR platform in the lab.

The goal is not just to have Wazuh installed and running, but to actually generate activity, see how it gets logged, understand what creates alerts, and learn how to troubleshoot when something does not show up the way I expect.

---

## 🔧 Current Setup

Wazuh is running inside my Proxmox environment and is connected to systems inside the lab.

Current systems and log sources include:

- Ubuntu Server
- Linux Mint
- Ubuntu Desktop
- pfSense firewall logs
- Additional lab systems as they are added

I’m continuing to expand the number of devices and services feeding data into Wazuh.

---

## 🧰 What I’m Using Wazuh For

Right now I’m using Wazuh for:

- Endpoint monitoring
- Centralized log collection
- Security alerting
- Vulnerability detection
- File integrity monitoring
- Event analysis
- Firewall log monitoring
- pfSense log ingestion
- Incident investigation
- Testing detection behavior

---

## 🔥 pfSense Integration

One of the bigger parts of this setup has been getting pfSense firewall logs into Wazuh.

This lets me generate traffic inside the lab, make firewall changes, and then check how that activity appears inside the SIEM.

I can use this to:

- Review allowed and blocked traffic
- Compare firewall behavior against expected results
- Test new firewall rules
- Check whether scans or unusual traffic are visible
- Confirm that events are being logged properly
- Troubleshoot parsing and decoding issues

This has been useful because I’m able to see the full path from network activity to firewall logs to SIEM alerts.

---
## 🚨 Custom Port Scan Detection

One of the better learning moments in the lab came from reviewing Wazuh logs and realizing I was getting an extremely high number of hits related to scanning activity.

Instead of just ignoring the noise, I went through the logs to understand what was generating the events and how the activity was being recorded.

From there, I planned, created, tested, and deployed a custom detection rule aimed at identifying possible port-scan behavior.

The process included:

- Reviewing Wazuh logs to identify the repeated scan activity
- Looking at the event patterns and source behavior
- Determining what information could be used to identify a possible scan
- Building a custom rule around that activity
- Testing the rule against traffic I generated in the lab
- Adjusting the rule based on the results
- Confirming Wazuh generated the expected alerts
- Deploying the rule into the active lab environment

This was useful because it moved the project beyond simply collecting logs.

I was able to take raw event data, identify a pattern, turn that pattern into detection logic, test it, and then use the rule in the live environment.

That gave me hands-on experience with the same basic detection-engineering process I want to keep building on in the lab:

**observe → analyze → build → test → tune → deploy**

---

## 🌍 Remote Testing and Validation

One of the most useful tests I’ve done was while traveling internationally.

Using Tailscale, I connected back into my lab from another country and used Kali Linux and Nmap to run authorized testing against my own lab systems.

During that testing, I was able to:

- Scan lab hosts with Nmap
- Check open ports and services
- Test subnet routing
- Test pfSense firewall behavior
- Write and apply firewall rules remotely
- Re-run scans after firewall changes
- Compare the activity I was generating with what showed up inside Wazuh
- Make sure Wazuh was actually seeing and alerting on the activity

This gave me a chance to test more than just remote access.

I was able to use Kali on the offensive side, pfSense on the defensive side, and Wazuh on the monitoring side, then compare all three to make sure the lab was behaving the way I expected.

That was one of the better real-world tests of the setup because I was doing it while physically outside of the country and still had full visibility into the lab.

---

## 🧪 Why I Built It This Way

I wanted a SIEM environment where the data was coming from systems I actually manage.

Instead of only working with pre-built logs or classroom examples, I can create activity myself and then go see what Wazuh does with it.

For example:

- Run an Nmap scan
- Check pfSense
- Review the firewall logs
- Check Wazuh
- See what alerts were generated
- Change a firewall rule
- Run the test again
- Compare the difference

That feedback loop is one of the main reasons I built the SIEM into the homelab.

It helps me understand what activity looks like from both the attacker and defender side.

---

## 🧠 What I’m Learning

Working with Wazuh has helped me get more hands-on with:

- Log analysis
- SIEM deployment
- Endpoint monitoring
- Firewall logging
- Alert validation
- Event correlation
- Linux logging
- Network traffic analysis
- Troubleshooting log ingestion
- Decoder and parser behavior
- Detection engineering concepts
- Incident-response workflows

It has also helped me understand how important visibility is.

Something happening on the network is only useful from a defensive point of view if I can actually see it, understand it, and determine whether it matters.

---

## 🚧 Current Projects

- [ ] Expand Wazuh agent coverage
- [ ] Improve pfSense log parsing
- [ ] Create more custom alerts
- [ ] Test additional detection rules
- [ ] Add more Linux endpoints
- [ ] Build repeatable attack/test scenarios
- [ ] Compare Nmap activity against Wazuh alerts
- [ ] Document alert examples
- [ ] Add screenshots of Wazuh dashboards
- [ ] Test file integrity monitoring
- [ ] Improve vulnerability monitoring
- [ ] Add more network-based log sources

---

## 📈 Future Goals

Things I want to do next:

- Create custom Wazuh rules
- Build better detection logic
- Add IDS/IPS data
- Add honeypot logs
- Create repeatable attack simulations
- Track alerts from start to finish
- Build simple incident-response playbooks
- Improve pfSense and Wazuh correlation
- Add dashboards for common attack activity
- Test brute-force detection
- Test port-scan detection
- Test suspicious login behavior
- Add more endpoints and services

---

## 🔄 SIEM Lab Philosophy

The main goal of this part of the lab is visibility.

I want to be able to create activity, understand what happened, see how it was logged, and figure out whether the SIEM caught it.

If Wazuh misses something, that gives me something to fix.

If it alerts on something useless, that gives me something to tune.

If it catches exactly what I expected, then I know that part of the setup is working.

That constant test, check, adjust, and re-test cycle is what makes this part of the homelab useful to me.
