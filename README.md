
# DVWA — Burp Suite Interception Lab

Author: Shelby (lab notes)



 Project summary

Goal: Configure Burp Suite and Firefox to intercept HTTP traffic for a local DVWA (Damn Vulnerable Web App) instance, document the troubleshooting process, and record lessons learned for future labs and portfolio use.

This repo documents a practical debugging session where DVWA pages loaded in the browser but Burp Suite did not capture the requests. The write-up shows step-by-step diagnosis, commands used, the final workaround (mapping a local domain to `127.0.0.1`), and takeaways about proxying and localhost traffic.


 Why this matters

Intercepting and inspecting local web app traffic is a fundamental skill for web application security testing. Understanding how browsers route local traffic and how proxies treat `localhost`/`127.0.0.1` helps avoid wasted time during pentesting labs and improves the ability to reproduce and debug issues in constrained environments.



