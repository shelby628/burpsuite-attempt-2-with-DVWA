burpsuite-attempt-2-with-DVWA
Installed Burp Suite • Installed Burp Suite Community Edition • Launched from terminal: • First Tests • Navigated to http://127.0.0.1/DVWA → DVWA loaded successfully • Tried accessing http://127.0.0.1/dvwa → Error: “URL not found on this server” ✅ Lesson: Linux URLs are case-sensitive

Proxy Configuration Steps Step-by-step Firefox Proxy Setup

Opened Firefox > Settings > Network Settings
Selected Manual Proxy Configuration
Set: o HTTP Proxy: 127.0.0.1 o Port: 8080 o Checked Use this proxy for all protocols
Confirmed setup using http://burp → saw Burp's helper page Verification • Opened about:support in Firefox Confirmed it's the right instance of Firefox that should use the proxy
Problem: DVWA Traffic Not Captured Despite all configurations: • DVWA pages loaded fine in Firefox • Burp did NOT capture the DVWA requests (only background requests like telemetry, Google) Captured Requests (from Burp HTTP history) Examples: GET https://www.google.com/complete/search?client=firefox... POST https://incoming.telemetry.mozilla.org/submit/firefox... But no http://127.0.0.1/DVWA/ or related traffic appeared

Root Cause Suspicions & Investigation Suspected Issue Investigated? Outcome Firefox not using proxy ✅ Yes Proxy confirmed working Proxy listener misconfigured ✅ Yes Listener working on 127.0.0.1:8080 Wrong browser being used ✅ Yes Verified with about:support Browser DNS bypass for localhost ✅ Yes Tried using IP instead of localhost Burp’s Intercept tab OFF ✅ Yes Intercept was ON DVWA accessed before proxy enabled ✅ Yes Reloaded page after proxy set Tests & Commands Used curl -x 127.0.0.1:8080 "http://127.0.0.1/DVWA" Result: Failed — Burp Suite may not intercept localhost by default Hostname Change Attempt • Tried replacing 127.0.0.1 with dvwa.local using /etc/hosts sudo nano /etc/hosts

127.0.0.1 dvwa.local Goal: Trick browser into routing through the proxy

Tips & What I Learned Key Takeaways

Burp doesn’t intercept localhost (127.0.0.1) by default. o You can’t capture traffic from localhost unless using a domain. o Workaround: Use a fake domain like dvwa.local mapped in /etc/hosts.
Linux paths are case-sensitive. o http://127.0.0.1/DVWA ≠ http://127.0.0.1/dvwa
Only traffic routed through a proxy-aware browser will appear in Burp. o Firefox must be properly configured
Verify everything step-by-step. o Browser config o Proxy listener o Intercept toggle o Test URLs manually
Remaining Questions • Why does Firefox exclude some localhost traffic from proxy? • Is there a Burp configuration to force capture of local traffic?

Final Reflection This was frustrating but valuable. Every time Burp didn’t work, I learned something new — about how traffic flows, how proxies behave, and how browsers handle local traffic. These lessons will definitely help when analyzing real-world web apps, especially those that use tricky routing or local testing environments.

In the end I was able to intercept dvwa traffic using burpsuite after several tries
