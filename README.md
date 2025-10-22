# Interface Tech Conference 2024 - Session Notes

***A collection of insights, technical deep-dives, and practical takeaways from the Interface Tech Conference held in Spokane, WA on October 16th 2025.***

---

## About This Repo

This October, I attended the Interface Tech Conference in Spokane. Rather than let my notes gather dust in a notebook somewhere, I wanted to create something more permanent and shareable.

Each session I attended offered unique perspectives on the challenges that all companies have to deal with: ransomware resilience, AI implementation that actually delivers value, zero trust architecture that doesn't break user experience, and the evolving threat landscape. These aren't theoretical discussions, but rather practitioners sharing what's working (and what's not) in production environments right now.

---

## Session Summaries

I've distilled each session into its own markdown file with the key insights, technical details, and practical takeaways:

| Sessions                                                                                                              | Key Takeaways                                                                                         |
|-----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| [Achieving Ransomware Resilience and Disaster Recovery in a Multi-Cloud World](./Achieving%20Ransomware%20Resilience%20and%20Disaster%20Recovery%20in%20a%20Multi-Cloud%20World.md) | Why backups fail against ransomware and what isolated recovery environments actually look like        |
| [How to Make AI a Reality in Your Organization](./How%20to%20Make%20AI%20a%20Reality%20in%20Your%20Organization.md)   | Moving from $10M proof-of-concepts that go nowhere to operational AI that creates business value      |
| [Bridging Zero Trust and SASE: A Unified Approach to Modern Cybersecurity](./Bridging%20Zero%20Trust%20and%20SASE%3A%20A%20Unified%20Approach%20to%20Modern%20Cybersecurity.md) | Balancing security and user experience without building an ivory tower                                |
| [AI in the Eyes of the Threat Actors vs. the Cyber Defense Line](./AI%20in%20the%20Eyes%20of%20the%20Threat%20Actors%20vs.%20the%20Cyber%20Defense%20Line.md) | What's actually happening vs the hype                                                                 |
| [Real-Time Threat Mitigation with AI-Driven SASE: A Practical Approach](./Real-Time%20Threat%20Mitigation%20with%20AI-Driven%20SASE%3A%20A%20Practical%20Approach.md) | Shadow AI, modern script kiddies, and why Layer 7 firewalls aren't enough anymore                     |
| [From Frameworks to Firewalls: A Practical Guide to AI Security](./From%20Frameworks%20to%20Firewalls%3A%20A%20Practical%20Guide%20to%20AI%20Security.md) | Practical AI security from OWASP Top 10 for LLMs to real CVEs like Echo Leak                          |

---

## Why These Topics Matter

If you're working in cloud infrastructure, security, or IT operations, you're probably dealing with some version of these challenges:

**The 18-22 day recovery problem** - Your backups won't save you from ransomware if they're on the network. The threat actors destroy those first.

**The AI implementation trap** - 8-month POCs that balloon from $1M to $10M with only 10% making it to production. Personal productivity ≠ business value.

**The user experience vs. security balance** - If you make zero trust too rigid, users will literally walk around your controls (sneakernet is real).

**The AI threat reality check** - Despite the hype, attackers are using AI as productivity tools, not generating polymorphic malware.. yet. But, they're well-funded ($100M/year for one ransomware group) and hiring top talent.

**The complexity problem** - LLMs are great at obfuscation. How do you fingerprint infinite iterations of the same malicious code?

---

## A Few Things That Stuck With Me

**On ransomware recovery:** "There are companies that make stuff to keep bad guys out. There are a few of us that make stuff to help you recover when the bad guys get in anyway." The assumption should be breach will happen—your recovery strategy matters more than ever.

**On AI projects:** Getting the final budget decision-maker in the room from day one isn't optional. Executive sponsorship that disappears after kickoff kills more AI projects than technical challenges.

**On zero trust:** "I wanna go fast, but I want to go fast with guardrails." Moving from 1975-era security to modern architecture requires speed AND stability. The ivory tower approach means missing the next wave entirely.

**On Shadow AI:** Overheard at Starbucks—someone casually mentioning they uploaded proprietary company data to their personal Claude account to generate a report. That's our new reality.

**On shared responsibility:** Every SaaS vendor is different. Always ask: "What is the SHARE?" Understanding your side of the shared responsibility model is foundational to everything else.

---

## How to Use These Notes

Each file is structured for quick reference:
- Executive summary up front
- Technical deep-dives in the middle
- Key quotes and takeaways throughout
- Actionable recommendations at the end

Whether you're preparing a security roadmap, evaluating AI initiatives, or just trying to stay current with the threat landscape, hopefully these notes save you some time and provide useful context.

---

## Acknowledgments

Thanks to all the speakers who shared their expertise—from the HPE team on ransomware resilience, to ImageSource on pragmatic AI implementation, the Fortinet panel on zero trust, Juniper's reality check on AI threats, Cato Networks on Shadow AI, and Structure Communications on AI security frameworks.

And thanks to the Interface organizers for creating a space where practitioners can share real-world experience rather than vendor pitches.

*These notes reflect my personal understanding, interpretation, and insights*

---

## Connect with Me

- **LinkedIn:** [https://www.linkedin.com/in/emilp-profile/](https://www.linkedin.com/in/emilp-profile/)
