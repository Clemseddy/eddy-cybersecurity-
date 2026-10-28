# h1-Cyberscience

## Sciencehunt

My interest area being cyber security threats in the banking and financial sector lead me to to find a solid scientific review article that examines corporate corruption, fraud antecedents, and organizational risk factors. moving down this assignment, I detail my search process (Part A), summarize a recent peer-reviewed scoping review on corporate corruption (Part B), and apply a threat modeling exercise to an imaginary digital banking company (Part C).

# A — Science Hunt
To find an appropriate review article, I followed the advice in Karvinen (2025) and conducted a search on Google Scholar. I used search terms related to course themes and my specific interest in financial integrity, specifically using the search string "banking fraud:review" as well as exploring related terms like corporate corruption and financial crime.

I selected the following peer-reviewed review article:
Selected Article:
- __Fornerod, L., Mugellini, G., & Villeneuve, J.-P. (2026). Corporate Corruption: A Scoping Review and a Dynamic Model of Its Antecedents. Journal of Business Ethics, https://doi.org/10.1007/s10551-026-06431-4__

I verified that the article meets all assignment criteria:
- Review Article Type: It is a comprehensive scoping review synthesizing 93 quantitative empirical studies on corporate corruption and fraud antecedents.
- Reputable Peer-Reviewed Journal: It is published in the Journal of Business Ethics (Springer Nature), a premier journal in business ethics and corporate governance.
- JUFO Rating: I checked the Publication Forum (JUFO) portal, and the Journal of Business Ethics is rated JUFO Level 2.
- Recency (<2 years old): The article was published online in August 2026, so it is brand new.
- Open Access: The full-text article is available open access, making it easily accessible.
My reason for choosing this article because corporate corruption and financial fraud are directly connected to threat modeling in organizations. Understanding why firms and employees engage in misconduct helps security professionals build better internal controls, threat models, and risk mitigation strategies.

# B — Review the Review
I read the scoping review by Fornerod et al. (2026) and summarized its key findings around the three required questions below.
## 1. What are the key areas being researched?
- Micro-Level (Individual Factors): Research examines executive and employee characteristics, including red tape interactions, personal financial need, executive position/duality, career ambitions, and psychological traits like narcissism, Machiavellianism, and moral rationalization techniques.
- Meso-Level (Organizational Factors): Studies analyze firm-specific drivers such as company size, age, ownership structure (family, state, insider, or foreign ownership), corporate governance, board diversity, internal control weaknesses, external audit quality, financial stress (leverage/liquidity), and industry competition.
- Macro-Level (Contextual Factors): Research investigates country-level influences including politico-legal institution strength, rule of law, democratic freedom, cultural dimensions (individualism vs. collectivism, power distance), press freedom, economic development, and regional corruption pervasiveness.
- Forms & Motives of Misconduct: The literature primarily focuses on bribery and financial fraud (accounting misstatements), while distinguishing between _need-driven_ corruption (coercion/extortion) and _greed-driven_ corruption (active pursuit of undue advantage or fraudulent gains).

## 2. What's widely agreed upon?
- Corporations are Active Participants: Scholars broadly agree that firms are active supply-side players in corrupt deals and financial misconduct, not merely passive victims of corrupt public officials.
- Multilevel Nature of Corruption: There is consensus that corporate corruption cannot be explained by single-level factors alone; it emerges from dynamic interactions across micro (individual), meso (organizational), and macro (environmental) levels.
- Governance and Audit Deterrence: Strong external auditing, rigorous internal controls (duty separation, whistleblowing channels), and diverse board monitoring consistently reduce the incidence and opportunity for corporate fraud and corruption.
- Pressure Increases Misconduct: Financial stress (high leverage, poor performance, liquidity constraints) and intense market competition create high performance pressure, significantly driving firms toward fraudulent accounting or bribe payouts.

## 3. What are the open questions?
- Disentangling Need vs. Greed: How can empirical research better separate coercive corruption ('need') from opportunistic fraud ('greed') when measuring organizational outcomes?
- Private-to-Private Corruption: How do corruption and fraud mechanisms operate in transactions purely between private companies (e.g., supply chain fraud, customer-salesperson collusion), which remain heavily understudied compared to firm-public official interactions?
- Cross-Level Dynamic Interactions: How do micro, meso, and macro drivers interact over time in dynamic 'spirals of corruption', and at which specific level can intervention strategies interrupt these spirals most effectively?
- Geographical and Methodological Gaps: Why do quantitative studies remain heavily clustered in Asia and North America, leaving regions like South America, Africa, and Oceania underrepresented? How can future research incorporate qualitative and process-oriented insights?

In my view, this scoping review highlights that internal security controls and threat modeling must account for human incentives, managerial pressure, and organizational culture. Technical controls alone are insufficient if organizational pressures incentivize employees or executives to bypass security procedures.

# C — Threat Modeling Quickrun
## Company Overview
Here i have taken into account an imaginary company which is FinTech Solutions Ltd., a mid-sized digital financial services provider. The FinTech solutions provides cloud-based payment gateways and API-driven digital banking integrations for approximately 150 corporate clients and e-commerce merchants.
## Crown Jewels
* Customer & Financial Data: Sensitive client account records, payment credentials, and transaction logs.
* Business Continuity: Uptime and operational availability of payment processing APIs and transaction settlement engines.
* Reputation: Client trust, brand integrity, and compliance standing with financial regulators.
* Money: Corporate treasury balances, client transaction funds, and operational liquidity.
## Bad Guys — COI (Capability, Opportunity, Intent)
Potential attackers include external cybercrime syndicates and compromised malicious insiders seeking financial gain.
- __Capability:__ Attackers possess advanced knowledge of web/API security, automated exploitation tools, credential stuffing scripts, and social engineering tactics to bypass authentication.
- __Opportunity:__ Exposed public payment APIs, administrative portals accessible over the internet, third-party software dependencies, or weak multi-factor authentication setup create attack vectors.
- __Intent:__ Attackers want direct financial gain through unauthorized wire transfers, extortion via service disruption, or selling compromised financial data on dark web markets.

## 2 examples of Risk Identification & Assessment
__Risk 1__ — Payment Gateway API Hijacking & Unauthorized Wire Fraud
Attackers exploit an unpatched API authentication flaw or compromise administrative credentials to inject unauthorized fund transfers into offshore accounts during non-business hours.
- Estimated Likelihood: 30% per year (0.30)
- Estimated Impact: €150,000 (comprising €110,000 in fraudulent transfers, €25,000 in forensic investigation/incident response, and €15,000 in regulatory/client notifications)
- Estimated Risk Value: 30% × €150,000 = €45,000

__Risk 2__ — Distributed Denial of Service (DDoS) Platform Outage
Attackers launch a large-scale volumetric DDoS attack against the payment gateway infrastructure, making the digital banking service unavailable for 24 hours.
- Estimated Likelihood: 50% per year (0.50)
- Estimated Impact: €40,000 (comprising €18,000 in lost transaction fee revenue, €12,000 in customer SLA penalties, and €10,000 in emergency technical mitigation)
- Estimated Risk Value: 50% × €40,000 = €20,000

__Risk Comparison Summary__

Risk Scenario	= Payment Gateway API Fraud;  Likelihood (%) = 30%; 	Impact (€) = €150,000; 	Estimated Risk (€) = €45,000

Risk Scenario	= DDoS Platform; Likelihood (%) = Outage; 	Impact (€) = 50%; Estimated Risk (€) = €40,000	€20,000

__Selection of Highest Priority Risk__
While a DDoS attack has a higher likelihood (50%), Payment Gateway API Fraud carries a significantly higher estimated financial risk (€45,000 vs. €20,000). Direct financial theft and fraud can cause catastrophic loss to the company's capital and client trust if undetected. Therefore, I select Risk 1 which is Payment Gateway API Fraud as the single biggest risk to address.
## Risk Treatment Decision (META Framework)
For the single biggest risk, I choose MITIGATE. Eliminating the risk is impossible because offering API-based payment processing is fundamental to our business model. Accepting or transferring the risk without active controls would expose the company to unacceptable financial destruction.

_Specific mitigation controls I will implement:_
- _Multi-Factor Authentication & Dual-Authorization:_ Require MFA for all administrative access and mandatory two-person approval (dual-authorization) for any wire transaction exceeding €10,000.
- _Automated Anomaly Detection:_ Deploy real-time transaction monitoring algorithms to detect unusual payment amounts, off-hours transfers, or unexpected recipient accounts.
- _API Security & Access Control:_ Enforce strict OAuth2 tokens, rate limiting, and quarterly penetration testing on payment gateway API endpoints.
- _Transaction Velocity Limits:_ Set hard daily transfer limits per account to prevent massive single-session losses if a account is breached.

By implementing these controls, the estimated likelihood drops from 30% to under 5%, and the maximum single-event impact is capped, effectively mitigating the threat to a manageable level. I hope i have been able to do my best with these imaginations. 

# References
Fornerod, L., Mugellini, G., & Villeneuve, J.-P. (2026). Corporate Corruption: A Scoping Review and a Dynamic Model of Its Antecedents. Journal of Business Ethics. https://doi.org/10.1007/s10551-026-06431-4

Karvinen, M. (2025). Start Your Research with a Review Article. Course Guidance Material.






