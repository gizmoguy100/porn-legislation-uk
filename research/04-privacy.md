# Dossier 04 — Privacy, security and data-protection vulnerabilities in the UK age-verification regime

**Prepared:** 2 November 2026  
**Scope:** Part 5, s81 Online Safety Act 2023 (pornographic content), with cross-reference to Part 3 children's duties and the UK GDPR / Data Protection Act 2018.  
**Method:** desk research — primary legislation, regulator guidance and statistics, parliamentary material, NGO reports, academic/technical literature and press reporting. Headline-level only on security incidents; no exploit mechanics.  
**Caveat:** this is an evidence dossier, not legal advice. Several sources are post-2025 and some are secondary reporting; quotes are reproduced as published, with ellipses where truncated.

---

## 0. The legal baseline — and why it is structurally weak

Section 81(4)(b) OSA 2023 requires a provider to make and keep a written record of:

> “the way in which the provider, when deciding on the kinds of age verification or age estimation and how they should be used, has had regard to the importance of protecting United Kingdom users from a breach of any statutory provision or rule of law concerning privacy that is relevant to the use or operation of a regulated service (including, but not limited to, any such provision or rule concerning the processing of personal data).”
>
> — Online Safety Act 2023, s 81(4)(b), https://www.legislation.gov.uk/ukpga/2023/50/section/81

Four features of the provision matter for the privacy analysis:

1. **It is a duty to “have regard”, not a duty to achieve an outcome.** There is no statutory privacy standard, no list of prohibited data types, no retention limit, no encryption requirement, no ban on secondary use, and no requirement to use privacy-preserving credentials. The provider must consider privacy; it need not minimise the privacy impact.
2. **It is decision-time and record-keeping only.** The duty attaches to “deciding on the kinds of age verification or age estimation and how they should be used”. It is not an ongoing operational security duty and does not expressly require post-procurement monitoring of a vendor.
3. **It protects against “breach of … law”, not against privacy intrusion as such.** Lawful but highly intrusive processing — a passport upload retained for 30 days, or a facial template sent to a US processor — can satisfy the duty if it complies with data protection law. The substantive standard is therefore whatever UK GDPR/DPA 2018 and the ICO say at the time.
4. **The public statement duty does not clearly cover the privacy reasoning.** Section 81(5) requires a public statement summarising the record “so far as the record concerns compliance with the duty set out in subsection (2)” — i.e. the age-verification duty — and “details about which kinds of age verification or age estimation a provider is using and how they are used”. On its face, the s 81(4)(b) privacy analysis can remain internal. This is our reading of the text; we found no regulator or court interpretation of the point.

Ofcom's own guidance confirms the light-touch design:

- “For an understanding of how to have regard to the importance of protecting users from a breach of any statutory provision or rule of law concerning privacy …, service providers should familiarise themselves with the data protection legislation, and how to apply it to their age assurance method. This includes by consulting ICO guidance and seeking relevant independent legal advice as service providers deem appropriate.” — Ofcom, *Guidance on highly effective age assurance*, para 5.2, https://www.ofcom.org.uk/siteassets/resources/documents/consultations/category-1-10-weeks/statement-age-assurance-and-childrens-access/part-3-guidance-on-highly-effective-age-assurance.pdf?v=427202
- “Where we have concerns that a provider has not complied with its obligations under data protection laws, we may refer the matter to the ICO.” — ibid, para 5.11.
- “To demonstrate compliance with this duty, service providers **may find it helpful** to include details of how they have taken privacy into account … in their written record.” — ibid, para 5.12 (emphasis added).

Open Rights Group's assessment is blunt: “Ofcom cannot mandate privacy standards within their existing OSA powers”; and “Section 81 duties should be redrafted in future legislation to ensure no impact to privacy and as minimal impact as possible on free expression.” — ORG, *Regulating Age Verification*, 23 July 2025, https://www.openrightsgroup.org/publications/regulating-age-verification/

**Bottom line:** the OSA creates a mass identity-checking infrastructure but delegates the privacy standard to a separate, differently-resourced regulator and to market choice. The s 81(4)(b) duty is a procedural overlay on a substantive gap.

---

## 1. Data honeypots: ID documents, selfies, biometric templates and financial data

**Description:** Age checks can require passports, driving licences, live selfies, facial templates, card details, bank records or mobile-network data. Centralising these in vendors creates high-value breach targets, and the appeal/fallback workflows are often less secure than the core check.

### What we found

- **Discord / 5CA — 70,000 government ID photos exposed (Sept–Oct 2025).** An unauthorised party compromised a third-party customer-service provider used to review age-related appeals. Discord confirmed “approximately 70,000 users that may have had government-ID photos exposed”. Exposed data also included names, usernames, emails, IP addresses, the last four digits of payment cards and support correspondence. Hackers claimed 2 million ID documents and 5.5 million users; Discord disputed the scale and called it an extortion attempt. 5CA said its systems were not hacked and pointed to human error by an employee. — *The Guardian*, 9 Oct 2025, https://www.theguardian.com/media/2025/oct/09/hack-age-verification-firm-discord-users-id-photos; *Computing*, Oct 2025, https://www.computing.co.uk/news/2025/security/discord-admits-compromise-of-70-000-online-safety-act-proof-of-age-ids
- **The breach was an over-retention story, not just a hacking story.** ID documents were being held in a customer-support ticketing system for appeal review — a workflow not designed for sensitive identity data. Biometric Update called it “over-retention of age verification data [having its] predictable result”. — *Biometric Update*, Oct 2025, https://www.biometricupdate.com/202510/over-retention-of-age-verification-data-has-predictable-result-in-discord-breach
- **Persona — 2,456 files and 269 verification checks exposed (Feb 2026).** Researchers found a publicly accessible Persona government-dashboard codebase (53 MB, 2,456 files) on a FedRAMP-authorised endpoint. The exposed code allegedly revealed 269 distinct verification checks, watchlist screening, and biometric face databases with three-year retention. Persona's CEO said it was a development instance, called the exposure “an oversight by the team”, and said “we do not work with any federal agency today” — while denying that it wants its technology used for surveillance. Discord subsequently dropped Persona and made k-ID its sole age-assurance vendor. — *Cybernews*, 19 Feb 2026, https://cybernews.com/privacy/persona-leak-exposes-global-surveillance-capabilities/; *Malwarebytes*, Feb 2026, https://www.malwarebytes.com/blog/news/2026/02/age-verification-vendor-persona-left-frontend-exposed
- **AU10TIX — admin credentials exposed for over a year (2024).** 404 Media reported that the identity-verification firm used by X, TikTok and Uber had administrative credentials online for more than a year, exposing images of driving licences and other ID documents. AU10TIX disputed that there was evidence of data exposure or customer impact. — *404 Media*, 2024, https://www.404media.co/id-verification-service-for-tiktok-uber-x-exposed-driver-licenses-au10tix/; *EFF*, June 2024, https://www.eff.org/deeplinks/2024/06/hack-age-verification-company-shows-privacy-danger-social-media-laws
- **Tea app — 72,000 verification images posted online (July 2025).** A US dating-safety app suffered a breach of about 72,000 images, including verification selfies, uploaded ID photos and app screenshots, posted on 4chan; a second breach exposed about 1.1 million private messages. The app was not acting under the OSA, but the breach coincided with the UK regime going live and illustrates the data pool created by verification selfies. — Kennedys Law, 22 Oct 2025, https://www.kennedyslaw.com/en/thought-leadership/article/2025/spilling-the-tea-on-id-risk-unintended-consequences-of-the-online-safety-act/
- **Most pornography services outsource the data.** Ofcom found that “almost all analysed pornography services relied exclusively on third-party vendors, with only one analysed pornography service using an in-house solution.” — Ofcom, *Report on the use of age assurance*, 15 July 2026, para 4.17, https://www.ofcom.org.uk/siteassets/resources/documents/online-safety/information-for-industry/age-assurance-report-2026/report-on-the-use-of-age-assurance.pdf?v=423162
- **Retention is short in the core check but variable.** Ofcom found one pornography service retaining facial images and ID documents for up to one hour; one social media service storing data for 72 hours and no more than 30 days; another reducing “photographic information” retention from seven to three days. Some services process only on-device and share a binary pass/fail. — ibid, paras 7.42–7.44.
- **Public concern is concentrated on data security.** Ofcom's “Proving Age” survey found that among lapsed pornography users who did not plan to return because of age checks, 94% identified at least one personal-data concern: 76% did not want to share personal information, 75% worried their information would not be protected, and 71% did not trust third-party providers. One participant: “there's no way I'm sticking my passport details in a random website.” — ibid, paras 7.55–7.61.
- **The vendor trade body concedes the weak point.** AVPA told the Lords that it was “not aware of a major data breach arising from the core privacy-preserving age-assurance transactions delivered by its members under the OSA”, but added that protections “must extend to fallback checks, customer support and appeals”. — AVPA, written evidence IOS0037, 7 Sept 2026, https://committees.parliament.uk/writtenevidence/169147/html/

**Status:** Multiple confirmed incidents; no age-assurance-specific security standard; the ICO has been assessing/investigating the Discord breach since Oct 2025, with the investigation reported as ongoing in Sept 2026; no public enforcement outcome against an age-assurance vendor in the UK.

**Gaps/unknowns:** the number of UK users affected in each incident; whether the ICO will fine Discord or 5CA; vendor security audit results; retention periods in appeal/support workflows across the market; the contractual allocation of controller/processor responsibility between platforms, vendors and subcontractors.

---

## 2. Vendor concentration and supply-chain risk

**Description:** A small number of age-assurance vendors sit behind a large share of UK checks. Concentration creates single points of failure, correlated breach exposure and commercial leverage over privacy terms.

### What we found

- **Yoti is the scale leader.** Yoti reported completing over one billion age checks globally by November 2025, across facial age estimation, digital IDs and ID-document checks. Secondary reporting puts it at roughly 500 million people by January 2026. — *Biometric Update*, Nov 2025, https://www.biometricupdate.com/202511/yoti-passes-a-billion-age-checks-building-foundation-of-trust; *Tech Insider*, 2026, https://tech-insider.org/yoti-vs-k-id-vs-persona-age-verification-2026/
- **Discord consolidated on k-ID after the Persona exposure.** k-ID became Discord's sole confirmed age-assurance vendor after the Persona episode; its “OpenAge” framework issues reusable “AgeKey” credentials. — *Tech Insider*, 2026 (above); *Biometric Update*, Nov 2025, https://www.biometricupdate.com/202511/with-openage-k-id-presents-itself-as-one-big-interoperable-solution-for-age-checks
- **Persona's customer base shows cross-platform concentration.** Persona is used by Reddit, was used in Discord's UK trial, and is also used by ChatGPT, Roblox and LinkedIn. A single vendor exposure therefore reaches many services and sectors. — *Cybernews*, 19 Feb 2026 (above); *PC Gamer*, Feb 2026, https://www.pcgamer.com/software/security/security-researchers-claim-persona-the-provider-behind-discords-uk-age-verification-experiment-performs-269-individual-verification-checks-on-user-data-including-those-for-terrorism-and-espionage/
- **Formal plurality, practical concentration.** AVPA represents “over 35 providers” of verification, estimation and inference. But Ofcom found that almost all pornography services rely exclusively on third-party vendors, and the average service offers three methods — meaning procurement decisions funnel through a much smaller set of suppliers. — AVPA, IOS0037, 7 Sept 2026 (above); Ofcom, 15 July 2026, para 4.17.
- **Supply chain extends beyond the age-check vendor.** The Discord breach entered through a customer-service provider (5CA) and its ticketing system, not through the facial-estimation vendor. The lesson is that the “age-assurance supply chain” includes support, appeals, hosting and analytics subcontractors. — *The Guardian*, 9 Oct 2025; Join the Claim, https://jointheclaim.com/discord-data-breach/
- **No public register or mandatory certification.** ORG notes there is “no public register of approved age assurance providers”, “no requirement for age assurance providers to meet any specific privacy or security standards”, and “no requirement for platforms to choose trusted or certified providers”. — ORG, press release, 23 July 2025, https://www.openrightsgroup.org/press-releases/org-calls-for-age-assurance-industry-to-be-regulated/
- **Ofcom's own remedy is due diligence, not structural regulation.** Its report tells services to “conduct regular and thorough due diligence on your age assurance vendors”, including checking configuration and metrics. This leaves concentration and continuity risk with the platform. — Ofcom, 15 July 2026, Section 8.
- **Ofcom recognises the single-point-of-failure problem elsewhere.** In its October 2026 app-store report it advocates “a layered or whole-of-system approach … avoiding any single point of failure” — but that logic is applied to app stores/device-level checks, not to the age-assurance vendor market. — Ofcom, 29 Oct 2026, https://www.ofcom.org.uk/online-safety/protecting-children/how-age-checks-at-age-16-can-work-to-underpin-uks-social-media-ban

**Status:** Market-led consolidation; no concentration limits, systemic designation, mandatory certification or public register; AVPA is asking for independent audit/certification against ISO/IEC 27566-1 and IEEE 2089.1.

**Gaps/unknowns:** market-share data by UK checks; the number of UK platforms per vendor; subcontractor maps; business-continuity and exit plans if a dominant vendor fails or is breached; whether platforms can switch vendors without re-collecting data.

---

## 3. The s 81(4)(b) privacy duty: is “have regard” too weak?

**Description:** The statutory privacy duty is procedural. Critics say it creates no enforceable privacy outcome and leaves the substantive standard to data protection law, which is separately and weakly enforced against age-assurance providers.

### What we found

- **The duty is textually thin.** It requires a written record of “the way in which” the provider “has had regard to the importance of protecting … from a breach of any statutory provision or rule of law concerning privacy”. It does not require minimisation, retention limits, security standards, interoperability or a DPIA; those come from UK GDPR and ICO guidance, not the OSA. — OSA 2023, s 81(4)(b).
- **The public statement may not disclose the privacy reasoning.** s 81(5) limits the public summary to the record “so far as the record concerns compliance with the duty set out in subsection (2)” — the age-verification duty — plus “details about which kinds of age verification or age estimation a provider is using and how they are used”. The privacy analysis in s 81(4)(b) is not expressly required to be published. (Our reading; no interpretive authority found.)
- **Ofcom treats privacy as a referral issue.** “Where we have concerns that a provider has not complied with its obligations under data protection laws, we may refer the matter to the ICO.” — Ofcom HEAA guidance, para 5.11. Ofcom's practical examples are permissive: a DPIA, privacy information, records of processing, policies, training and documented security measures — things providers “may find it helpful” to include. — ibid, paras 5.12–5.13.
- **ORG says the OSA cannot deliver privacy standards.** “Ofcom cannot mandate privacy standards within their existing OSA powers”; the Act relies “solely” on data protection law and creates commercial incentives for “cheap technology providers” and data monetisation. ORG's recommendation 32 is to redraft s 81 “to ensure no impact to privacy”. — ORG, *Regulating Age Verification*, 23 July 2025.
- **ORG says data-protection enforcement is not a credible deterrent.** “Breaches of data protection law are rarely if ever enforced against by the UK's Information Commissioner, with the exception of spam and cold calling. This means that companies are not running a financial risk even if they seriously break data protection rules.” — ibid.
- **Big Brother Watch frames the regime as a digital-ID wedge.** “There is a broad spectrum of age checking methods, including dangerously intrusive methods like biometric face scans and even ID cards and passports for internet access. We must avoid anything like a digital ID system for the internet that would both eradicate privacy online and fail to keep children safe.” — Big Brother Watch, 16 Jan 2025, https://bigbrotherwatch.org.uk/press-releases/big-brother-watch-responds-to-risky-age-verification-measures-online/
- **Privacy International emphasises structural, irreversible risk.** “Age-verification schemes introduce structural risks that cannot be mitigated merely by assurances from vendors or platform operators… Biometric data is especially valuable — unlike a password, your face and fingerprints cannot be changed. Once they have been hacked, you cannot get them back.” — Privacy International, 2026, https://www.privacyinternational.org/news-analysis/5737/discord-pushes-back-age-verification-after-security-risks-revealed
- **Index on Censorship links privacy to anonymity and expression.** It warns that age verification threatens “some degree of online anonymity or pseudonymity” and that “the fallibility of technology means that the privacy of us all could be compromised”. — Index on Censorship, July 2025, https://www.indexoncensorship.org/2025/07/free-expression-concerns-over-online-safety-acts-age-verification-requirements/; Aug 2025, https://www.indexoncensorship.org/2025/08/the-online-safety-act-risks-making-everyone-less-safe-online/
- **5Rights accepts age assurance but demands privacy by design.** “Age assurance measures must be secure and must align with children's privacy rights and data protection law. Additionally, they must abide by the principles of data minimisation and purpose limitation and remain robust over time.” — 5Rights, *Age Assurance as a spectrum*, Feb 2026, https://5rightsfoundation.com/wp-content/uploads/2026/02/5rights_AgeAssurance_FINAL.pdf
- **The ICO says both regimes apply, but does not give the OSA duty independent content.** The ICO/Ofcom joint statement says compliance with online safety and data protection is “mandatory and should not be considered a trade-off”, and lists data minimisation, storage limitation, purpose limitation, transparency, fairness and accountability. Those are UK GDPR duties, not new OSA duties. — ICO/Ofcom, *Age Assurance: A Joint Statement*, 25 Mar 2026, https://ico.org.uk/media2/5ybpmabf/ofcom-ico-joint-statement.pdf

**Status:** No amendment; the Government has declined to regulate age-assurance providers (ORG, Sept 2026); ORG, with AVPA and over 600 public signatories, wrote to the Secretary of State in Dec 2025 and re-publicised the call in Feb 2026; the Lords Communications and Digital Committee is inquiring into the OSA's implementation and impact, with a report still outstanding as of 2 Nov 2026.

**Gaps/unknowns:** no Ofcom or court interpretation of s 81(4)(b); no public audit of providers' s 81 records; no dataset on how many s 81(5) statements actually discuss privacy; no dedicated parliamentary committee report on the privacy duty; the “1 in 10 under-16s lack a passport” figure in the brief was not verified in official sources (see §6).

---

## 4. The ICO's role and guidance: strong on paper, tilted toward more age assurance

**Description:** The ICO has produced detailed age-assurance guidance and is enforcing failures to age-assure, but it has not published enforcement against an age-assurance vendor for over-collection, retention or reuse.

### What we found

- **The ICO's Age Assurance Opinion sets substantive expectations.** It requires a lawful basis, purpose limitation, data minimisation, accuracy, storage limitation, security and accountability; says age-assurance data must not be reused for advertising or profiling; requires a DPIA before processing special-category biometric data; and states: “In many cases it may be excessive to see an official document (eg a passport or driving licence)… You may only need to record a yes or no output that a person meets the age threshold.” — ICO, *Age assurance for the Children's code*, section 6, https://ico.org.uk/about-the-ico/what-we-do/information-commissions-opinions/age-assurance-for-the-children-s-code/6-expectations-for-age-assurance-and-data-protection-compliance/
- **It recognises exclusion and bias.** “Age verification usually depends on the user having ready access to official documents or a credit history. Young adults and people from disadvantaged backgrounds … may have lower rates of access to a driver's licence or passport”; age estimation “may not perform as well for people of darker skin tones, or those with medical conditions or disabilities that affect physical appearance”. — ibid, section 6.3.3.
- **It warns about parental routes.** “The use of parental controls, such as account confirmation for the purposes of age assurance, pose risks to a child's privacy. These should only be used where the child has authorised the parent to do this, the child doesn't have sufficient understanding to exercise the rights themselves or it is evident that this is in the best interests of the child.” — ICO, age assurance guidance, https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/how-to-use-our-guidance-for-standard-one-best-interests-of-the-child/best-interests-framework/age-assurance/
- **The ICO and Ofcom issued a joint statement (25 March 2026).** It says age assurance must be risk-based, flexible and technology-neutral; services must apply data protection principles; and a DPIA is expected where processing is high-risk. — ICO/Ofcom joint statement, 25 Mar 2026, https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/2026/03/joint-statement-from-ico-and-ofcom-on-age-assurance/
- **The ICO's enforcement is aimed at under-verification, not over-collection.** On 24 Feb 2026 it fined Reddit £14.47m for failing to apply “any robust age assurance mechanism” and for failing to carry out a DPIA; on 5 Feb 2026 it fined MediaLab (Imgur) £247,590 for similar failures. The direction of travel is more age assurance, not less data collection. — ICO, 24 Feb 2026, https://ico-newsroom.prgloo.com/news/ico-issues-reddit-with-gbp-14-47m-fine-for-childrens-privacy-failures; *Biometric Update*, 24 Feb 2026, https://www.biometricupdate.com/202602/ico-hits-reddit-with-14-5m-fine-for-not-implementing-robust-age-assurance
- **The ICO says it is assessing providers.** In October 2026 it said: “This also complements our own work assessing how age assurance providers currently comply with data protection law.” No findings, audits or enforcement outcomes have been published. — ICO, 29 Oct 2026, https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/2026/10/ico-statement-on-highly-effective-age-assurance/
- **The ICO has an audit toolkit but no published age-assurance provider audit.** The toolkit sets control measures on method selection, security, statistical accuracy, transparency, challenge/human review and third-party contracts. It is guidance for organisations, not a public audit programme. — ICO, *Data protection audit framework: Age assurance*, https://ico.org.uk/for-organisations/advice-and-services/audits/data-protection-audit-framework/toolkits/age-appropriate-design/age-assurance/
- **Certification is voluntary.** The ICO approved the Age Check Certification Scheme (ACCS) in 2021; applying is voluntary. ORG says voluntary standards are “insufficient” and wants mandatory certification. — ICO opinion, section 6.2; ORG, 23 July 2025.
- **The ICO's guidance is in flux.** Pages carry a notice that, owing to the Data (Use and Access) Act, the guidance “is under review and may be subject to change”. — ICO opinion pages, accessed 2 Nov 2026.

**Status:** Detailed guidance and platform enforcement; provider assessment announced but unpublished; no UK fine or audit of an age-assurance vendor for privacy breaches; voluntary certification only.

**Gaps/unknowns:** the scope and results of the ICO's provider assessment; whether the ICO can effectively regulate US-based vendors; resourcing and enforcement appetite; whether the ICO will treat “over-collection” as seriously as “under-verification”; the effect of the Data (Use and Access) Act on the Children's code.

---

## 5. Facial age estimation: bias, accuracy near thresholds and the adequacy of Ofcom's “fairness” criterion

**Description:** Facial age estimation is the least data-intensive method at scale, but its error rates are highest around the age thresholds that matter, and performance varies by skin tone, sex and age. Ofcom's fairness criterion is self-assessed and expressly excludes exclusion caused by lack of ID.

### What we found

- **Ofcom defines fairness narrowly.** “Fairness describes the extent to which an age assurance method avoids or minimises bias and discriminatory outcomes. It refers here to the **internal operation** of an age assurance method, **rather than external factors, such as a lack of access to a particular form of identification** required by the age assurance method, which are covered by the principles below.” — Ofcom HEAA guidance, para 4.51 (emphasis added).
- **The test is outcome/error parity, self-certified.** Providers should “consider and monitor the outcome / error parity across different characteristics (such as race and sex)” and “should be satisfied that the results indicate that the age assurance method(s) does not produce significant bias or discriminatory outcomes.” There is no numeric threshold, no mandated independent test and no publication requirement. — ibid, paras 4.54–4.58.
- **NIST data shows the scale of error.** For ages 13–17 the lowest mean absolute error among tested algorithms is 1.77 years; 19 of 50 algorithms are below 3 years. For 18–25 the lowest MAE is 2.39 years; 9 of 50 are below 3 years. — Ofcom, *Rapid assessment … at 16*, 29 Oct 2026, paras 3.21–3.22, https://www.ofcom.org.uk/siteassets/resources/documents/online-safety/protecting-children/rapid-assessment-of-highly-effective-age-assurance-at-16.pdf?v=427159
- **Near-threshold error is the design problem.** “If the facial age estimation algorithm is accurate within two years for children aged 15, it could estimate them as aged 17. This could result in significant numbers of children under 16 gaining access… It could also result in a 17-year-old being denied access if they are estimated to be 15.” Ofcom's answer is a “challenge age” buffer, which shifts friction onto 16–19-year-olds. — ibid, paras 3.23–3.26.
- **The Australian trial found very high false-positive rates for children.** At a 16+ threshold, false-positive rates (a child wrongly estimated to be over 16) were 25.2% for under-13s, 38.3% at 13, 59.4% at 14 and 73.3% at 15; combined error rates at 16, 17 and 18 were 13.9%, 8.7% and 2.4% respectively. — *The Guardian*, 19 Sept 2025, https://www.theguardian.com/news/2025/sep/19/how-accurate-are-age-checks-for-australias-under-16s-social-media-ban-what-trial-data-reveals
- **The same trial found racial bias but the report downplayed it.** “The trial's analysis of skin tone showed that age estimation systems had a higher error rate on average for people with darker skin. However, because no group had 20% more errors than the average, the report concluded: ‘This indicates no significant evidence of adverse impact or systemic disparity in error rates across skin tone groups…’” The Guardian notes the ACCS report did not publish accuracy rates by demographic background despite holding the raw data. — ibid.
- **The UK Government's own study accepts bias.** “Despite significant progress in FAE accuracy, tools still struggle to distinguish users within narrow age bands (e.g. under 13 or under 18) and exhibit bias across gender, skin tone, ethnicity.” The main barrier is “limited availability of high-quality, representative training and testing datasets, especially for children”; the market is unlikely to resolve this alone. — DSIT, *Age Assurance Data Access Study*, 26 Mar 2026, https://www.gov.uk/government/publications/age-assurance-data-access-study/age-assurance-data-access-study
- **Parliament's POST note summarises the vendor and Government positions.** Yoti reports MAE of 1.2 years for ages 6–12 and 1.3 for 13–17; DSIT says “even with 1–2 years average error, this means that there are cases where a 12-year-old could be mistaken for 14, or a 16-year-old for 18”. The Home Office notes variation by “ethnicity, skin tone, gender, place of birth and quality of input image”. — POST, *Facial age estimation*, https://post.parliament.uk/facial-age-estimation/
- **Academic work shows error and bias are often conflated.** A 2026 *Nature* paper argues the conventional accuracy metric is “confounded by response bias”; AI models underestimate older adults and show larger biases than humans in some age bands. — *Nature*, 2026, https://www.nature.com/articles/s41598-026-49573-1
- **Accessibility is a separate fairness problem.** Ofcom accepts that users may be unable to complete facial checks without a smartphone/tablet with a working camera, and that users with special educational needs and disabilities may face “more barriers” in multi-step processes. — Ofcom, *Rapid assessment*, para 3.31.

**Status:** Ofcom acknowledges the limits but has not set a quantitative fairness threshold, mandated independent demographic testing or taken enforcement action on bias. The “fairness” criterion is a process expectation, not a performance standard.

**Gaps/unknowns:** UK-specific, post-deployment error rates by skin tone, sex, age and disability for the vendors actually used; false-rejection rates and appeal outcomes; whether providers publish NIST results for the exact model deployed; intersectional bias; performance on low-quality cameras and in poor lighting; whether “challenge age” settings are audited.

---

## 6. ID exclusion and digital exclusion

**Description:** ID-based checks exclude people without passports, licences or credit histories, disproportionately the young, the poor, the disabled and people in care. Ofcom's fairness criterion expressly does not cover this; it is only an “accessibility principle”.

### What we found

- **Photo ID coverage is high but not universal.** “An estimated 94% of people aged 16 and over in the UK have either a passport or driving licence. Evidence suggests around 150,000 16- and 17-year-olds in the UK have neither.” The estimate comes from a CitizenCard non-representative school survey of 8,459 respondents. — Ofcom, 29 Oct 2026, https://www.ofcom.org.uk/online-safety/protecting-children/how-age-checks-at-age-16-can-work-to-underpin-uks-social-media-ban
- **Bank accounts cover more 16–17s than photo ID.** “Evidence suggests around 90% of UK 16- to 17-year-olds hold a bank account.” — ibid.
- **But photo ID is likely needed at some point in every “highly effective” route at 16.** Ofcom accepts that “a photo ID will likely be needed at some point in the process”, either for the method itself, to open a bank account, or to obtain a digital ID. — Ofcom, *Rapid assessment*, para 3.33.
- **Deprivation predicts passport ownership.** “In England, 21.2% of those in the most deprived areas do not have a passport compared to 7.1% in the least deprived.” Young people in the care system, particularly short-term placements, are less likely to have photo ID. — ibid, para 3.32 and n.55.
- **The ICO recognises the discrimination risk.** Hard identifiers “provide a high level of certainty” but “also have a higher risk of discrimination”; third-party verification risks “indirectly discriminating against people who lack the necessary documentation or data, such as credit history”. — ICO, Children's code FAQs, https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/faqs-on-the-15-standards-of-the-children-s-code/
- **EFF frames this as an access-to-information problem.** “Age verification laws that are predicated on the necessity of users possessing a current passport, driver's license, credit card, or similar documents proving their identity exclude critical sections of populations… The UK has a similar predicament.” — EFF, 8 Oct 2026, https://www.eff.org/deeplinks/2026/10/when-no-id-means-no-internet-age-verification-and-right-access-information
- **Ofcom's “fairness” criterion does not cover this.** It is expressly limited to the “internal operation” of the method, “rather than external factors, such as a lack of access to a particular form of identification”. Exclusion is relegated to the “accessibility” principle, which providers only “should consider”. — Ofcom HEAA guidance, para 4.51 and section 4.
- **The proposed mitigation is a PASS card.** Ofcom notes that 16–17s can apply for a passport, provisional licence or a PASS-certified photo ID card, with free PASS cards available for 16–17s. It does not assess take-up, cost, waiting times or whether platforms will accept them. — Ofcom, 29 Oct 2026, n.6.
- **Digital exclusion compounds ID exclusion.** Facial estimation requires a camera-equipped smartphone or tablet; bank-based checks require online banking; digital IDs require a smartphone and a enrolment journey. Ofcom acknowledges these barriers but does not quantify them. — Ofcom, *Rapid assessment*, paras 3.30–3.31.

**Status:** Ofcom acknowledges exclusion and recommends PASS cards; we found no published equalities impact assessment, no mandated alternative route, and no duty on platforms to offer a non-ID method. The “fairness” criterion does not capture exclusion.

**Gaps/unknowns:** a robust UK estimate of adults without any accepted ID; the specific “1 in 10 under-16s lack a passport” claim was not located in official sources (closest official figures are the 94%/150,000/21.2% figures above); PASS-card take-up and acceptance; waiting times and costs; data on disabled, homeless, care-experienced and digitally excluded users; whether platforms offer offline or assisted routes.

---

## 7. Linkability, re-verification and age tokens

**Description:** Repeated checks create linkability and friction. Privacy-preserving credentials (zero-knowledge proofs, reusable age tokens, digital wallets) can reduce data sharing, but the OSA does not mandate them, and centralised token issuers create new correlation and single-point-of-failure risks.

### What we found

- **The OSA does not mandate privacy-preserving credentials.** s 81 requires “age verification or age estimation” that is “highly effective”; it says nothing about zero-knowledge proofs, selective disclosure, unlinkability or reusable tokens. The only privacy hook is the s 81(4)(b) “have regard” duty.
- **Ofcom's interoperability principle is not a duty.** “In the context of age assurance, interoperability may involve re-using the result of an age check across multiple services… Service providers can have regard to interoperability by staying up to date with developments in this area, and considering whether to implement interoperable solutions to age assurance where they exist and are appropriate for the service.” — Ofcom HEAA guidance, paras 4.69–4.72.
- **ORG confirms Ofcom cannot mandate it.** “Ofcom's guidance can make reference to the ‘principle’ of interoperability, ie users choosing their own AV tool, but Ofcom cannot mandate it.” — ORG, 23 July 2025.
- **Industry is building reusable credentials.** AVPA's OpenAge initiative, launched by k-ID, uses an “AgeKey” — “a privacy-preserving digital credential that lets users prove that they meet an age threshold without revealing their identity”, supporting zero-knowledge proofs and selective disclosure. OpenAge says “over 10 million seamless verifications” were completed during its beta phase, and publishes ISO/IEC 27001, 27701 and 27566 certifications and a SOC 2 Type 2 attestation. — OpenAge Initiative, https://www.openageinitiative.org/; AVPA, https://avpassociation.com/interoperable-age-assurance/
- **The EU's own app shows the security risk of centralised tokens.** Within hours of launch in April 2026, researchers bypassed the EU age-verification app's protections in under two minutes: rate-limiting was stored in an editable file, biometric authentication was controlled by a single boolean, and credentials were accessible without secure hardware. A researcher later demonstrated replaying the same “over-18” token via a Chrome extension. The zero-knowledge features were not enabled in the production build. — Proton, 20 Apr 2026, https://proton.me/blog/eu-age-verification-app-hacked; EFF, 18 Aug 2026, https://www.eff.org/deeplinks/2026/08/zkps-arent-age-verification-silver-bullets
- **EFF argues ZKPs centralise power rather than removing it.** “The idea behind ZKPs is that you are issued a ‘token’ that vouches for your age every time you log in, creating a constant link back to the entity that verified you. The issuer of the tokens these AV schemes rely on could track every time that credential was used, creating a dangerous trail of metadata on any user they wanted to target.” — EFF, 18 Aug 2026.
- **EDRi says unlinkability is hard to guarantee.** “If the central authority in charge of the system is technically able to connect data points, privacy disasters will quietly unfold every time it will be breached, subpoenaed, or if it ever acts maliciously.” — EDRi, 2026, https://edri.org/our-work/eu-age-verification-tool-does-not-solve-privacy-concerns/
- **Hundreds of researchers want a moratorium.** More than 400 (later 438) security and privacy researchers signed an open letter calling for a pause on age-assurance deployment until the science settles. — https://csa-scientist-open-letter.org/ageverif-Feb2026
- **The UK is moving toward device/app-store-level age signals.** Ofcom's October 2026 app-store report says app stores could reduce repeated checks, but “would not absolve the social network providers from doing their own checks as well”; it advocates a “layered or whole-of-system approach”. The Government's digital ID work would create a reusable age attribute for public and private services, with children aged 13+ eligible. — Ofcom, 29 Oct 2026; GOV.UK digital identity consultation, https://www.gov.uk/government/consultations/making-public-services-work-for-you-with-your-digital-identity/making-public-services-work-for-you-with-your-digital-identity

**Status:** Market-led; no mandate for reusable or privacy-preserving credentials; OpenAge/AgeKey is growing but voluntary; the EU app's flaws have strengthened the case for caution; UK digital ID policy is still developing.

**Gaps/unknowns:** take-up and coverage of reusable credentials in the UK; whether major porn sites accept third-party age tokens; the linkability properties of AgeKey and similar credentials (independent audit?); whether the UK digital ID will become a de facto mandatory age signal; data-protection impact of app-store/device-level attestation; cross-border recognition.

---

## 8. Children's and parents' data: parental consent, retention and deletion

**Description:** Age assurance processes children's data as well as adults'. Parental consent and “account holder confirmation” routes pull parents into the data flow, while retention and deletion are governed by general data protection law rather than any age-assurance-specific rule.

### What we found

- **The ICO accepts that age assurance processes children's data.** “When assessing the age of your users, you are likely to be processing both adults' and children's personal information. Data protection law requires you to protect everyone's personal information.” — ICO opinion, section 6.
- **Under-13 consent requires parental authorisation.** The ICO says it is “unlawful to process information of children under 13 if there is no evidence of consent from someone with parental responsibility”, because only children aged 13+ can consent for information-society services under Article 8 UK GDPR. — ibid, section 6.1.6.
- **Parental confirmation routes create their own privacy risk.** “The use of parental controls, such as account confirmation for the purposes of age assurance, pose risks to a child's privacy. These should only be used where the child has authorised the parent to do this, the child doesn't have sufficient understanding to exercise the rights themselves or it is evident that this is in the best interests of the child.” — ICO, age assurance guidance (above).
- **Parents should not automatically exercise children's rights.** The ICO says parents should only exercise rights on a child's behalf if the child authorises it, lacks understanding, or it is in the child's best interests. — ICO opinion, section 6.1.3.
- **Retention is “minimum necessary”, not a fixed period.** “You must retain only the minimum amount of personal information necessary for the purpose. If you use a hard identifier to assess age, you may only need to retain a yes or no output once you've completed the check.” — ibid, section 6.1.7.
- **Actual retention varies widely.** Ofcom found examples of one hour for facial images and ID documents, 72 hours/30 days for a social media service, and a reduction from seven to three days for “photographic information”. Some services process only on-device and share a binary pass/fail. — Ofcom, 15 July 2026, paras 7.42–7.44.
- **Parents' top concern is privacy.** Internet Matters research cited by Ofcom found privacy was the top concern for parents (43%), followed by uncertainty about how data is used (35%). — Ofcom, 15 July 2026, para 7.59.
- **Global sweep finds weak age assurance and poor deletion.** GPEN's 2026 sweep of 876 websites/apps found 45% deployed some age assurance; sweepers could circumvent age assurance in 72% of cases (460/641), most often where self-declaration was used. It also flags concerns about children's data collection, lack of child-specific privacy information, and absence of an accessible way to delete accounts. — GPEN, *Children's Privacy Sweep Report*, Mar 2026, https://www.privacyenforcement.net/system/files/2026-03/GPEN%20Sweep%20Report%20-%20March%202026%20-%20EN.pdf
- **5Rights insists on data minimisation and purpose limitation.** “Age assurance measures must be secure and must align with children's privacy rights and data protection law… data minimisation and purpose limitation… remain robust over time.” — 5Rights, Feb 2026 (above).

**Status:** Children's code and UK GDPR apply; under-13 parental consent is required; there is no age-assurance-specific retention limit, no statutory deletion deadline and no published data on parental-route data flows.

**Gaps/unknowns:** how much parent/guardian data is collected and retained in parental-verification routes; whether platforms verify that a “parent” is actually the holder of parental responsibility; deletion verification; children's data held by vendors versus platforms; age-assurance of under-13s on pornography sites (where the user should not be there at all); whether “account holder confirmation” is being used as a backdoor to avoid robust checks.

---

## 9. Security incidents, CVEs and regulator findings

**Description:** Age-assurance vendors hold exactly the data attackers want. The public record shows repeated incidents, but there is no age-assurance-specific security standard, incident register or vulnerability-disclosure regime.

### What we found

- **Discord / 5CA (2025):** ~70,000 government ID photos; support-ticket data; ICO assessing/investigating; UK group-action registration and a US consolidated class action. — *The Guardian*, 9 Oct 2025; Join the Claim, https://jointheclaim.com/discord-data-breach/
- **Persona (2026):** 2,456 files/53 MB exposed on a FedRAMP endpoint; researchers allege 269 verification checks and three-year biometric retention; Persona says development instance and “oversight”; Discord dropped Persona. — *Cybernews*, 19 Feb 2026; *Malwarebytes*, Feb 2026.
- **AU10TIX (2024):** administrative credentials exposed for over a year; images of driving licences of X/TikTok/Uber users; company denies evidence of exposure. — *404 Media*, 2024; *EFF*, June 2024.
- **Tea app (2025):** ~72,000 verification images (selfies, IDs, screenshots) posted on 4chan; ~1.1 million private messages in a second breach; multiple lawsuits. — Kennedys Law, 22 Oct 2025.
- **EU age-verification app (2026):** bypassed in under two minutes; rate-limiting editable; biometric flag; credentials outside secure enclave; token replay; ZKP not enabled in production. — Proton, 20 Apr 2026; EFF, 18 Aug 2026.
- **CVE record is thin and mostly unrelated to major vendors.** An NVD keyword search for “age verification” returns 65 CVEs, overwhelmingly WordPress age-verification plugins (e.g. CVE-2024-55979/55980 SQL injection; CVE-2025-7401 arbitrary file read/write; CVE-2025-22622; CVE-2025-29004). We found no public CVE for Yoti, Persona, k-ID or other major UK-facing vendors. — NVD API search, 2 Nov 2026, https://services.nvd.nist.gov/rest/json/cves/2.0?keywordSearch=age%20verification
- **Ofcom's liveness data shows basic controls are uneven.** Of 29 services using facial age estimation, 25 explicitly referenced liveness detection; two used video selfies without saying so; two were “exploring” liveness. Retry limits and cooldowns are used but not universal. — Ofcom, 15 July 2026, Annex 2, paras A2.17–A2.18.
- **AVPA says the core transactions are clean but the edges are not.** It is “not aware of a major data breach arising from the core privacy-preserving age-assurance transactions”, but says protections “must extend to fallback checks, customer support and appeals”. — AVPA, IOS0037, 7 Sept 2026.

**Status:** Confirmed incidents; no mandatory security certification for age-assurance vendors; no public incident register; GDPR breach-reporting applies; the ICO's Discord investigation is ongoing; no published enforcement outcome against a vendor.

**Gaps/unknowns:** under-reporting; the number of UK users affected; whether vendors have vulnerability-disclosure programmes; security audit results; supply-chain subcontractor lists; whether platforms test vendor configuration changes; the security of appeal/support workflows; CVE coverage of proprietary code.

---

## 10. Litigation and regulatory action on privacy grounds

**Description:** Privacy-based litigation is emerging, but mostly in the US and Spain. There is no UK judicial review or damages award testing s 81(4)(b), and Ofcom has not taken privacy enforcement action.

### What we found

- **Spain fined Yoti €950,000 (March 2026).** The AEPD found Yoti breached GDPR Articles 5(1)(e) (excessive retention), 7 (invalid consent) and 9 (unlawful biometric processing) in its Digital ID app: biometric matching was treated as special-category processing without a valid Article 9 condition; users “consent by default” to R&D use; geolocation was retained for five years; liveness videos for 30 days; fraudulent ID documents were retained to train software. Fines: €250,000 + €200,000 + €500,000. Yoti says the decision concerns only its Spanish Digital ID app, not its processor services, and has appealed to the Spanish High Court. — *Biometric Update*, 11 Mar 2026, https://www.biometricupdate.com/202603/spains-aepd-fines-yoti-1-1m-for-biometric-data-handling-violations; AEPD decision, https://www.aepd.es/documento/ps-00164-2025.pdf; Yoti response, https://www.yoti.com/blog/thoughts-from-our-ceo-march-2026/
- **UK group-action registration for the Discord breach.** Join the Claim is gathering UK users who may have had ID photos exposed; as of Sept 2026 it says the ICO investigation “remains on-going”; the claim remains at “register your interest” stage and no issued UK proceedings are reported. — https://jointheclaim.com/discord-data-breach/
- **US consolidated class action.** A consolidated complaint against Discord and 5CA was filed in a California federal court in February 2026. It is separate from any UK claim and does not establish liability. — ibid.
- **ICO enforcement is not privacy-protective in direction.** Reddit (£14.47m, Feb 2026) and Imgur/MediaLab (£247,590, Feb 2026) were fined for failing to age-assure and failing to carry out DPIAs — i.e. for processing children's data without adequate age checks. Neither is a penalty for over-collection or retention by an age-assurance vendor. — ICO, 24 Feb 2026; *Addleshaw Goddard*, 13 May 2026, https://www.addleshawgoddard.com/en/insights/insights-briefings/2026/technology/age-verification-ico-vs-ofcom-who-will-take-lead/
- **No UK judicial review on privacy grounds was located.** We found no challenge to the OSA age-verification regime, Ofcom's guidance or s 81(4)(b) on Article 8/UK GDPR grounds. The academic literature discusses the privacy/expression tension but not a live UK case. — Search of parliamentary, regulatory and press sources, 2 Nov 2026.
- **No Ofcom privacy enforcement.** Ofcom's OSA enforcement to date concerns failure to implement age checks (e.g. fines against 8579 LLC and Kick), not privacy failures; its guidance says it “may refer” privacy concerns to the ICO. — Ofcom HEAA guidance, para 5.11; *Biometric Update*, Feb 2026.

**Status:** Yoti's Spanish appeal pending; ICO Discord investigation ongoing; UK group action at registration stage; no UK privacy-based JR or damages award; no Ofcom privacy sanction.

**Gaps/unknowns:** whether the Yoti appeal changes the retention/consent analysis; whether the ICO will fine Discord/5CA; whether a UK group claim will be funded and issued; whether any platform has been challenged on its s 81(4)(b) record; the prospect of a UK GDPR representative action against a US vendor.

---

## 11. Cross-cutting assessment

| Issue | Evidence strength | Regulatory action to date | Direction of travel |
|---|---|---|---|
| Data honeypots / breach risk | **Strong** — multiple confirmed incidents | ICO investigating Discord; no vendor fine | Worsening as volumes grow |
| Vendor concentration | **Moderate** — scale data, no market-share data | None; voluntary certification | Consolidating |
| s 81(4)(b) weakness | **Strong on text; moderate on critique** | No amendment; Lords inquiry | Static / possible legislative fix |
| ICO role | **Strong on guidance; weak on enforcement** | Platform fines; provider assessment unpublished | More age assurance, not less data |
| Facial bias / fairness | **Strong** — NIST, DSIT, Australian trial | No enforcement; no numeric threshold | Incremental accuracy gains; bias persists |
| ID exclusion | **Strong on 16–17s; weaker on adults** | PASS-card recommendation | Unresolved |
| Linkability / tokens | **Moderate** — technical and policy literature | No mandate; market-led | Reusable credentials growing |
| Children's / parents' data | **Moderate** — guidance and retention examples | Children's code applies | Unresolved parental-route risks |
| Security incidents / CVEs | **Strong on incidents; thin on CVEs** | No AV-specific regime | Under-regulated |
| Litigation | **Moderate** — Spain fine, US/UK claims | Yoti appeal; ICO investigation | Early stage |

**The central finding:** the UK regime has created a mandatory, population-scale identity-verification market without a mandatory privacy or security standard. The s 81(4)(b) duty is a procedural obligation to *consider* privacy and *record* that consideration; it is not a substantive privacy standard, and the public statement duty may not even require the privacy reasoning to be published. The substantive protections are UK GDPR/DPA 2018, enforced by the ICO — a regulator that is currently using its powers mainly to require *more* age assurance, not to restrain data collection by age-assurance vendors.

---

## Source list

### Primary legislation and regulator guidance
1. Online Safety Act 2023, s 81 — https://www.legislation.gov.uk/ukpga/2023/50/section/81
2. Online Safety Act 2023, s 82 — https://www.legislation.gov.uk/ukpga/2023/50/section/82
3. Ofcom, *Guidance on highly effective age assurance* (Part 3), 2025 — https://www.ofcom.org.uk/siteassets/resources/documents/consultations/category-1-10-weeks/statement-age-assurance-and-childrens-access/part-3-guidance-on-highly-effective-age-assurance.pdf?v=427202
4. Ofcom, *Age assurance duties under the Online Safety Act* — https://www.ofcom.org.uk/online-safety/protecting-children/age-assurance
5. Ofcom, *Report on the use of age assurance* (s 157 report), 15 July 2026 — https://www.ofcom.org.uk/siteassets/resources/documents/online-safety/information-for-industry/age-assurance-report-2026/report-on-the-use-of-age-assurance.pdf?v=423162
6. Ofcom, *Rapid assessment of highly effective age assurance at 16*, 29 Oct 2026 — https://www.ofcom.org.uk/siteassets/resources/documents/online-safety/protecting-children/rapid-assessment-of-highly-effective-age-assurance-at-16.pdf?v=427159
7. Ofcom, *How age checks at age 16 can work to underpin UK's social media ban*, 29 Oct 2026 — https://www.ofcom.org.uk/online-safety/protecting-children/how-age-checks-at-age-16-can-work-to-underpin-uks-social-media-ban
8. Ofcom, *Age checks: Why their placement matters in pornography*, 14 Jan 2026 — https://www.ofcom.org.uk/online-safety/protecting-children/age-checks-why-their-placement-matters-in-pornography
9. ICO, *Age assurance for the Children's code* (Commissioner's Opinion), section 6 — https://ico.org.uk/about-the-ico/what-we-do/information-commissions-opinions/age-assurance-for-the-children-s-code/6-expectations-for-age-assurance-and-data-protection-compliance/
10. ICO, *Age assurance* (Children's code guidance) — https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/how-to-use-our-guidance-for-standard-one-best-interests-of-the-child/best-interests-framework/age-assurance/
11. ICO, *FAQs on the 15 standards of the Children's code* — https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/faqs-on-the-15-standards-of-the-children-s-code/
12. ICO, *Open letter to social media and video sharing platforms on strengthening age assurance*, Mar 2026 — https://ico.org.uk/about-the-ico/open-letter-to-social-media-and-video-sharing-platforms-on-strengthening-age-assurance
13. ICO/Ofcom, *Age Assurance: A Joint Statement*, 25 Mar 2026 — https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/2026/03/joint-statement-from-ico-and-ofcom-on-age-assurance/ ; PDF: https://ico.org.uk/media2/5ybpmabf/ofcom-ico-joint-statement.pdf
14. ICO, *Data protection audit framework: Age assurance* — https://ico.org.uk/for-organisations/advice-and-services/audits/data-protection-audit-framework/toolkits/age-appropriate-design/age-assurance/
15. ICO, *Children's code strategy progress update — December 2025* — https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/protecting-childrens-privacy-online-our-childrens-code-strategy/children-s-code-strategy-progress-update-december-2025/
16. ICO, *ICO issues Reddit with £14.47m fine for children's privacy failures*, 24 Feb 2026 — https://ico-newsroom.prgloo.com/news/ico-issues-reddit-with-gbp-14-47m-fine-for-childrens-privacy-failures
17. ICO, *ICO statement on age assurance*, 21 May 2026 — https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/2026/05/ico-statement-on-age-assurance/
18. ICO, *ICO statement on Highly Effective Age Assurance*, 29 Oct 2026 — https://ico.org.uk/about-the-ico/media-centre/news-and-blogs/2026/10/ico-statement-on-highly-effective-age-assurance/

### Parliament and Government
19. House of Lords Communications and Digital Committee, *The Online Safety Act: implementation and impact* — https://committees.parliament.uk/work/9955/the-online-safety-act-implementation-and-impact/
20. AVPA, written evidence IOS0037, 7 Sept 2026 — https://committees.parliament.uk/writtenevidence/169147/html/
21. DSIT, *Age Assurance Data Access Study*, 26 Mar 2026 — https://www.gov.uk/government/publications/age-assurance-data-access-study/age-assurance-data-access-study
22. POST, *Facial age estimation* — https://post.parliament.uk/facial-age-estimation/
23. GOV.UK, *Making public services work for you with your digital identity* (consultation) — https://www.gov.uk/government/consultations/making-public-services-work-for-you-with-your-digital-identity/making-public-services-work-for-you-with-your-digital-identity
24. TechTimes, *Lords Open Online Safety Act Inquiry as Breach-Prone Age Checks Strip Adult Privacy*, 28 July 2026 — https://www.techtimes.com/articles/321819/20260728/lords-open-online-safety-act-inquiry-breach-prone-age-checks-strip-adult-privacy.htm

### NGOs and civil society
25. Open Rights Group, *Regulating Age Verification*, 23 July 2025 — https://www.openrightsgroup.org/publications/regulating-age-verification/
26. Open Rights Group, *ORG calls for age assurance industry to be regulated*, 23 July 2025 — https://www.openrightsgroup.org/press-releases/org-calls-for-age-assurance-industry-to-be-regulated/
27. Open Rights Group, *Break privacy to make privacy? Age verification isn't the answer*, 17 Mar 2026 — https://www.openrightsgroup.org/blog/break-privacy-to-make-privacy-age-verification-isnt-the-answer/
28. Open Rights Group, *Online Safety Act: Age assurance industry must be regulated*, 12 Dec 2025 — https://www.openrightsgroup.org/press-releases/online-safety-act-org-calls-for-regulation-of-age-assurance-industry/
29. Open Rights Group, *Online harms: Millions could be forced to use unregulated age verification*, 16 Feb 2026 — https://www.openrightsgroup.org/press-releases/online-harms-millions-could-be-forced-to-use-unregulated-age-verification/
30. Open Rights Group, *How to Fix the Online Safety Act: A Rights First Approach*, 15 May 2025 — https://www.openrightsgroup.org/publications/how-to-fix-the-online-safety-act-a-rights-first-approach/
31. Big Brother Watch, *Big Brother Watch Responds to Risky Age Verification Measures Online*, 16 Jan 2025 — https://bigbrotherwatch.org.uk/press-releases/big-brother-watch-responds-to-risky-age-verification-measures-online/
32. Privacy International, *Discord pushes back age verification after security risks revealed*, 2026 — https://www.privacyinternational.org/news-analysis/5737/discord-pushes-back-age-verification-after-security-risks-revealed
33. Index on Censorship, *Free expression concerns over Online Safety Act's age verification requirements*, July 2025 — https://www.indexoncensorship.org/2025/07/free-expression-concerns-over-online-safety-acts-age-verification-requirements/
34. Index on Censorship, *The Online Safety Act risks making everyone less safe online*, Aug 2025 — https://www.indexoncensorship.org/2025/08/the-online-safety-act-risks-making-everyone-less-safe-online/
35. 5Rights Foundation, *Age Assurance as a spectrum*, Feb 2026 — https://5rightsfoundation.com/wp-content/uploads/2026/02/5rights_AgeAssurance_FINAL.pdf
36. EFF, *When No ID Means No Internet*, 8 Oct 2026 — https://www.eff.org/deeplinks/2026/10/when-no-id-means-no-internet-age-verification-and-right-access-information
37. EFF, *Zero-Knowledge Proofs Aren't Age Verification Silver Bullets*, 18 Aug 2026 — https://www.eff.org/deeplinks/2026/08/zkps-arent-age-verification-silver-bullets
38. EFF, *Hack of Age Verification Company Shows Privacy Danger of Social Media Laws*, June 2024 — https://www.eff.org/deeplinks/2024/06/hack-age-verification-company-shows-privacy-danger-social-media-laws
39. EDRi, *Why the EU age-verification tool does not solve privacy concerns*, 2026 — https://edri.org/our-work/eu-age-verification-tool-does-not-solve-privacy-concerns/
40. GPEN, *Children's Privacy Sweep Report*, Mar 2026 — https://www.privacyenforcement.net/system/files/2026-03/GPEN%20Sweep%20Report%20-%20March%202026%20-%20EN.pdf
41. AVPA, *Interoperable Age Assurance* — https://avpassociation.com/interoperable-age-assurance/
42. AVPA, *OpenAge Initiative* — https://avpassociation.com/openage-initiative/ ; OpenAge Initiative — https://www.openageinitiative.org/
43. Open letter of 438 security and privacy researchers on age assurance, Feb 2026 — https://csa-scientist-open-letter.org/ageverif-Feb2026

### Incidents, technical analysis and litigation
44. *The Guardian*, *Hack of age verification firm may have exposed 70,000 Discord users' ID photos*, 9 Oct 2025 — https://www.theguardian.com/media/2025/oct/09/hack-age-verification-firm-discord-users-id-photos
45. *Computing*, *Discord admits compromise of 70,000 Online Safety Act proof-of-age IDs*, Oct 2025 — https://www.computing.co.uk/news/2025/security/discord-admits-compromise-of-70-000-online-safety-act-proof-of-age-ids
46. *Biometric Update*, *Discord partner's manual age verification data breach includes selfies*, Oct 2025 — https://www.biometricupdate.com/202510/discord-partners-manual-age-verification-data-breach-includes-selfies
47. *Biometric Update*, *Over-retention of age verification data has predictable result in Discord breach*, Oct 2025 — https://www.biometricupdate.com/202510/over-retention-of-age-verification-data-has-predictable-result-in-discord-breach
48. *Cybernews*, *Firm that verifies mugshots for ChatGPT and Roblox feeds US surveillance apparatus with 269 distinct checks*, 19 Feb 2026 — https://cybernews.com/privacy/persona-leak-exposes-global-surveillance-capabilities/
49. *Malwarebytes*, *Age verification vendor Persona left frontend exposed*, Feb 2026 — https://www.malwarebytes.com/blog/news/2026/02/age-verification-vendor-persona-left-frontend-exposed
50. *PC Gamer*, *Security researchers claim Persona … performs 269 individual verification checks*, Feb 2026 — https://www.pcgamer.com/software/security/security-researchers-claim-persona-the-provider-behind-discords-uk-age-verification-experiment-performs-269-individual-verification-checks-on-user-data-including-those-for-terrorism-and-espionage/
51. *404 Media*, *ID Verification Service for TikTok, Uber, X Exposed Driver Licenses*, 2024 — https://www.404media.co/id-verification-service-for-tiktok-uber-x-exposed-driver-licenses-au10tix/
52. Kennedys Law, *Spilling the tea on ID risk: Unintended consequences of the Online Safety Act*, 22 Oct 2025 — https://www.kennedyslaw.com/en/thought-leadership/article/2025/spilling-the-tea-on-id-risk-unintended-consequences-of-the-online-safety-act/
53. Proton, *The EU's age verification app was hacked in two minutes*, 20 Apr 2026 — https://proton.me/blog/eu-age-verification-app-hacked
54. Join the Claim, *Discord data breach* — https://jointheclaim.com/discord-data-breach/
55. *Biometric Update*, *Spain's AEPD fines Yoti $1.1M for biometric data handling violations*, 11 Mar 2026 — https://www.biometricupdate.com/202603/spains-aepd-fines-yoti-1-1m-for-biometric-data-handling-violations
56. AEPD, decision PS-00164-2025 — https://www.aepd.es/documento/ps-00164-2025.pdf
57. Yoti, *Thoughts from our CEO: Spanish regulator AEPD fining Yoti*, Mar 2026 — https://www.yoti.com/blog/thoughts-from-our-ceo-march-2026/
58. *Biometric Update*, *Yoti passes a billion age checks*, Nov 2025 — https://www.biometricupdate.com/202511/yoti-passes-a-billion-age-checks-building-foundation-of-trust
59. *Biometric Update*, *ICO hits Reddit with £14.5M fine for not implementing robust age assurance*, 24 Feb 2026 — https://www.biometricupdate.com/202602/ico-hits-reddit-with-14-5m-fine-for-not-implementing-robust-age-assurance
60. Addleshaw Goddard, *Age verification: ICO vs Ofcom, who will take the lead?*, 13 May 2026 — https://www.addleshawgoddard.com/en/insights/insights-briefings/2026/technology/age-verification-ico-vs-ofcom-who-will-take-lead/

### Accuracy and bias literature
61. *The Guardian*, *Social media ban trial data reveals racial bias in age checking software*, 19 Sept 2025 — https://www.theguardian.com/news/2025/sep/19/how-accurate-are-age-checks-for-australias-under-16s-social-media-ban-what-trial-data-reveals
62. *Nature*, *A new framework for facial age estimation in humans and AIs*, 2026 — https://www.nature.com/articles/s41598-026-49573-1
63. *Nature*, *Biases in human perception of facial age are present and more exaggerated in current AI technology*, 2022 — https://www.nature.com/articles/s41598-022-27009-w
64. MIT News, *Study finds gender and skin-type bias in commercial artificial-intelligence systems*, 2018 — https://news.mit.edu/2018/study-finds-gender-skin-type-bias-artificial-intelligence-systems-0212
65. NVD CVE keyword search, “age verification”, accessed 2 Nov 2026 — https://services.nvd.nist.gov/rest/json/cves/2.0?keywordSearch=age%20verification
