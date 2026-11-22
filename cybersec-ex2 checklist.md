I’d revise this before submitting, but you already have enough material. The strongest passage is where you say your _initial idea_ was that a test credential might work in production, then explain what would have to be true for that to happen. That sounds like someone thinking through their own findings. I’d use that passage as the model for the weaker ones.

I reviewed the assignment, the report, the appendices, and relevant evidence in the project history. I made no changes. **Items 1–10 are the ones I’d address before submission.** Most involve replacing or cutting text.

## Submission checklist

- [ ] 
    
    **1. Make the certificate section consistent with the passive-recon assignment.** You describe “requesting a fresh check” through SSLShopper, then conclude that your findings came from existing public records. The lecture notes allow browsing and mention third-party scanners, while the written brief asks what an attacker can learn without sending probes. Say how you actually obtained each result. Label the Chrome screenshot as a browser observation. If you requested a fresh test, say so and keep it outside the evidence for your passive findings. There’s an easy replacement in your project history: the saved Cert Spotter response contains the exact certificate fingerprint shown in Chrome, plus `login-admin-test.eldorado.gg` and `*.qa-test.eldorado.gg`. Put those three records in a small appendix extract and link to it. That also fixes the reference to a nonexistent “certificate transparency records” section. A wildcard is evidence of a certificate name only. [Certificate section (line 173)](C:/dev/cybersec-osint/report.md:173) · [Broken reference (line 388)](C:/dev/cybersec-osint/report.md:388) · [Assignment wording (line 44)](C:/dev/cybersec-osint/exercise.md:44)
    
    To inspect the saved source, run `git show cfb899a:evidence/2026-11-04/certspotter-page-2.json` and search for record IDs `18045132540` (Chrome match), `17423548747` (admin-test), and `17402267349` (QA wildcard).
    
- [ ] 
    
    **2. Finish both Recon-ng TODOs with one comparison.** Your project history already contains a **4 November** Recon-ng transcript. I checked two rows: `www.eldorado.gg → 104.18.6.75` and `airbyte.eldorado.gg → 34.44.191.208`. Both agree with your DNSDumpster appendix. The `www` pair also appears in your current mnemonic JSON, making it a useful independent cross-check. DNSDumpster and HackerTarget share an operator. The Recon-ng module returns hostname/IP pairs. For the ASN, your DNSDumpster and Shodan entries both give **AS396982** for the Airbyte address. Attribute each part to the source that actually supplied it. Two sentences and a linked transcript excerpt can close both TODOs. [First TODO (line 65)](C:/dev/cybersec-osint/report.md:65) · [Second TODO (line 256)](C:/dev/cybersec-osint/report.md:256) · [Recon-ng module](https://github.com/lanmaster53/recon-ng-marketplace/blob/master/modules/recon/domains-hosts/hackertarget.py) · [DNSDumpster’s provider information](https://dnsdumpster.com/membership/)
    
    Read the original with `git show cfb899a:evidence/2026-11-04/recon-ng/session.txt`. If you want to reproduce it yourself, open Recon-ng and enter the following. It searches HackerTarget’s existing host records. Keep the date and values your run actually returns. [HackerTarget dataset](https://hackertarget.com/find-dns-host-records/)
    
    ```
    workspaces create eldorado_review
    spool start eldorado-review.txt
    marketplace install recon/domains-hosts/hackertarget
    modules load recon/domains-hosts/hackertarget
    options set SOURCE eldorado.gg
    run
    back
    db query SELECT host, ip_address FROM hosts WHERE module = 'hackertarget' AND host IN ('www.eldorado.gg', 'airbyte.eldorado.gg')
    spool stop
    ```
    
- [ ] 
    
    **3. Correct the Shodan claim that the Lightdash host “has two vulnerabilities.”** Your own evidence lists two _potential_ CVEs for an IP where Shodan observed NGINX on port 80. For example, CVE‑2025‑23419 requires a particular TLS configuration, including TLS 1.3 and session resumption. The HTTP observation establishes neither condition. I’d keep that one example and cut the repeated CVE descriptions. Apply the same care to `internal-test`: Shodan saw Azure Front Door at the IP. The job advert supports company use of .NET, but it cannot identify what runs behind that particular endpoint. [Lightdash claim (line 152)](C:/dev/cybersec-osint/report.md:152) · [Azure claim (line 138)](C:/dev/cybersec-osint/report.md:138) · [Shodan’s explanation](https://help.shodan.io/mastery/vulnerability-assessment) · [NGINX advisory](https://mailman.nginx.org/pipermail/nginx-announce/2025/NYEUJX7NCBCGJGXDFVXNMAAMJDFSE45G.html)
    
- [ ] 
    
    **4. Give the first attack path a specific starting point and ending.** The conclusion calls it “data-tool connections,” while the section itself ranges from Angular to PHP2Shell to hijacking transactions. Your own Airbyte finding gives you a tighter argument. The hostname suggests a data integration. An attacker would first need access to the tool or a valid credential. The connection’s permissions would then determine which data they could read or change. A defender could check who can reach the tool and what its accounts can access. That fits all five questions in the brief and makes the conclusion accurate. Cut PHP2Shell because you found no evidence of PHP. I’d also cut the early jump from a test hostname to XSS and point readers to your much better test-credential discussion later. [First attack path (line 369)](C:/dev/cybersec-osint/report.md:369) · [Early XSS claim (line 43)](C:/dev/cybersec-osint/report.md:43) · [Conclusion (line 414)](C:/dev/cybersec-osint/report.md:414)
    
- [ ] 
    
    **5. Correct what the historical DNS timeline establishes.** Your 22-record count and table dates agree with the raw appendix. The interpretation underneath loses a more interesting result: **mnemonic saw Cloudflare addresses in March 2022, while it still observed an Azure Front Door CNAME as late as May 2023.** Those observations overlap. Describe the public-facing delivery services observed for `www` and leave the exact migration date and backend hosting open. Apply that correction to “cloud hosting of choice is likely Cloudflare” too. You can also combine the two adjacent IPv6 rows: the long and compressed forms represent the same three addresses. [DNS table and interpretation (line 235)](C:/dev/cybersec-osint/report.md:235) · [Hosting claim (line 375)](C:/dev/cybersec-osint/report.md:375) · [Cloudflare’s explanation of proxy addresses](https://developers.cloudflare.com/fundamentals/concepts/cloudflare-ip-addresses/)
    
- [ ] 
    
    **6. Update the merger finding.** You correctly read the 2021 notice as a proposal. There are also later official notices that answer the question you left open. Registrų centras records that **Atlantis LT was deregistered on 17 February 2022 and Mavericks Media on 18 February 2022**, both following reorganization. Keep the original notice identifying Eldorado as the intended successor and replace “no documents about it actually taking place were found” with the two dated outcomes. That is a substantive improvement in one sentence. [Report passage (line 69)](C:/dev/cybersec-osint/report.md:69) · [Original proposal](https://www.registrucentras.lt/jar/infleid/download.do?oid=206662#page=6) · [Atlantis LT notice 5366395](https://www.registrucentras.lt/jar/infleid/download.do?oid=224564) · [Mavericks Media notice 5368588](https://www.registrucentras.lt/jar/infleid/download.do?oid=224565)
    
- [ ] 
    
    **7. Fix the email interpretation.** Both MX lists point to Google. Google documents the single `smtp.google.com` setup and the older multi-server setup, so you can report agreement on the provider while leaving the reason for the differing snapshots open. SPF concerns who may send **email** for the domain. It says nothing about push notifications, and `_spf.newsletter.eldorado.gg` alone cannot tell you who operates a server. Cut those deductions and the suggestion that an attacker would take over an “SPF server.” Your later example of a compromised sending account already gives a realistic consequence. If you keep the DKIM/DMARC recommendation, make clear which controls you actually checked. [Email section (line 264)](C:/dev/cybersec-osint/report.md:264) · [Google’s MX documentation](https://knowledge.workspace.google.com/admin/domains/set-up-mx-records-for-google-workspace) · [SPF specification](https://www.rfc-editor.org/rfc/rfc7208)
    
- [ ] 
    
    **8. Remove three inferences a lecturer can challenge from the report itself.** The introduction says looser regulation makes vulnerabilities easier to find and cybercrime easier to get away with. Your reason for choosing a marketplace that handles valuable transactions stands on its own. The engineering section subtracts roughly 50 technical staff from 239/240 employees to suggest 190 phishing targets. Those figures describe different dates and potentially different groups, and neither source measures susceptibility to phishing. Finally, the same paragraph says BuiltWith identified EF Core. Your BuiltWith list says **ASP.NET Core**. **EF Core** came from the engineering article. Keep that distinction and date the job listing when citing Angular 20. [Introduction (line 5)](C:/dev/cybersec-osint/report.md:5) · [Engineering comparison (line 332)](C:/dev/cybersec-osint/report.md:332) · [Eldorado’s January 2026 engineering article](https://engineering.eldorado.gg/architecture-without-architects-how-we-build-at-eldorado-gg-4a1243f1e239)
    
- [ ] 
    
    **9. Make the conflicting and negative results verifiable.** For `hub.eldorado.gg`, one section says USA and the other says Frankfurt. Identify what each source reported and leave the physical server location unresolved. For “Google … doesn’t bring up any search results,” give the query, date, and narrower outcome: whether you found a credible disclosure about **this** Eldorado. Your saved search notes contain `eldorado.gg data breach` and `Eldorado Market breach`. For changing pages such as Shodan and the job advert, a dated excerpt in the appendix will let the lecturer verify the specific version or port you cite. If you use new research surfaced by this review, include that use in the brief AI disclosure the lecture requests. [RIPEstat entry (line 53)](C:/dev/cybersec-osint/report.md:53) · [Shodan entry (line 109)](C:/dev/cybersec-osint/report.md:109) · [Incident search (line 363)](C:/dev/cybersec-osint/report.md:363) · [Grading requirement (line 78)](C:/dev/cybersec-osint/exercise.md:78)
    
- [ ] 
    
    **10. Check the submitted ZIP from the lecturer’s side.** The Appendix A image currently points to `certificate.png`, but the actual file is `appendix/certificate.png`. The earlier inline link is correct. The two heading links on line 332 also contain spaces after `#`. If you keep those links, use `#web-technologies` and `#osint-report-of-eldorado-market`. Extract the finished ZIP into a fresh folder, open `report.md` in preview, and click the figure and evidence links. The older Recon-ng and Cert Spotter files are currently available in Git history only, so include the excerpts you cite in the ZIP itself. [Figure (line 418)](C:/dev/cybersec-osint/report.md:418) · [Heading links (line 332)](C:/dev/cybersec-osint/report.md:332)
    

## If time remains

- [ ] **Do one short typo pass.** Search for `path version` → `patch version`, `Clouflare` → `Cloudflare`, `BuildWith` → `BuiltWith`, `reconnasance` → `reconnaissance`, `shouldn;t` → `shouldn’t`, and `publically` → `publicly`. These are easy corrections that preserve your phrasing.
- [ ] **Trim repeated Shodan commentary if you want to shorten the report.** Sentences that repeat “ports 80 and 443 are open” immediately after the port list can go. I’d keep the sentences where you noticed something yourself, especially the conflicting locations, overlapping DNS dates, and conditions for reusing a test credential. Those are the parts I’d remember as your lecturer.