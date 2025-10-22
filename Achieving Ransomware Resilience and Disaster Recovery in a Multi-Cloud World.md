# Achieving Ransomware Resilience and Disaster Recovery in a Multi-Cloud World

**Presented by:** Mike Dusche, HPE

---

## The Fundamental Problem

### Facilities Outage vs. Ransomware Attack

**Facilities Outage:**
- You still have clean backups
- Straightforward recovery process
- Recovery time: 4-7 days

**Ransomware Attack:**
- Bad actors destroy your backups FIRST
- Recovery time: 18-22 days minimum
- Much more complex and expensive

> **Core Insight:** "The biggest difference is when there's a facilities based outage, you still have good pristine backups. When there's a ransomware attack, there's a bad actor and he or she is not going to let you get back up."

---

## Real-World Costs: Why This Matters

### Financial Impact

| Organization | Cost per Hour Down |
|--------------|-------------------|
| Regional hospitals (Spokane-sized) | $10-15M |
| United Airlines | $10M |

### Human Impact

**Major Metropolitan Police Department:**
- **27-35 lives lost** if systems down >8 hours
- Cannot track emergency responses
- Lose coordination capabilities

### Case Studies

#### MGM Grand Casino
- **Downtime:** 6 weeks
- **Attack vector:** One of the IT guys logged in to his email on his wife's laptop, and a hacker used LinkedIn and hacked her deivce and had access to his email
- **Lesson:** Attack surfaces are everywhere

#### Kentucky Hospital (Name Confidential)
- **Attack type:** Altered patient records (not deleted)
- **Impact:** Unpredictable number of records changed
- **Risk:** Life-threatening - wrong treatments administered
- **Example:** Patient needs dialysis, gets sugar instead

---

## Why Traditional Backups Fail for Ransomware

### The Modern Backup Problem

**Original Design:**
- Tapes stored offline (Iron Mountain, vaults)
- Physically disconnected from network
- Safe from network-based attacks

**Today's Reality:**
- Backups stored on disk
- Connected to network for quick recovery
- Designed for speed: "CFO deleted a file, wants it back PDQ"
- **Vulnerable to the same attacks as production systems**

### The Fundamental Flaw

> **Key Quote:** "If it's on a network, they'll get to it. Anything that's on a network, I'll find it. I'm not even that good anymore, but there's people like [Kevin Mitnick] that can attack anything that's on a network, period, the end."

### Eight Critical Backup Vulnerabilities

1. **Network connectivity makes backups targets**
   - Ransomware attacks
   - One may not even notice they're gone until too late

2. **Immutable ≠ Indestructible**
   - Immutable files can't be changed
   - But they CAN be destroyed
   - Common misconception

3. **Cloud backups get deleted daily**
   - AWS, Azure, GCP all vulnerable
   - "Hundreds of times each day files get deleted by hackers"
   - It's a network like any other

4. **Data proximity problem**
   - Moving 300TB from cloud takes WEEKS
   - Physics can't be overcome
   - Time-to-recovery unacceptable

5. **FBI equipment quarantine**
   - Government seizes equipment for forensics
   - Can't use it until investigation complete
   - Adds days/weeks to recovery timeline

6. **Unclean recovery points**
   - Attack may have been ongoing for months
   - Finding clean backup requires binary search backward
   - Each scan takes days

7. **Keys on network compromise immutability**
   - If encryption keys are network-accessible
   - "Immutable" files can be compromised

8. **Long recovery process**
   - Not just restore time
   - Scanning, validation, sanitization required

---

## The 18-22 Day Recovery Timeline

### Breakdown (Based on IDC Data, 2 Petabyte Archive)
```
Day 0:  Attack discovered
Day 9:  Remediation can BEGIN (planning, assessment)
Day 11: Forensic analysis complete (+2 days)
Day 18: Environment sanitized (+7 days)
Day 18-22: Ready to begin actual recovery
```

**Note:** Mike considers 18 days "ambitious" - likely longer in practice

### Why So Long?

**Days 1-9: Can't Even Start**
- Assessing damage
- Planning response
- Coordinating with stakeholders
- Legal/FBI involvement

**Days 9-11: Forensic Analysis**
- Scan archives for malware
- Identify clean recovery point
- May require multiple attempts
- "Oops, that was not good. Let's go back the day before"

**Days 11-18: Sanitization**
- Assuming FBI gives clearance
- Clean the environment
- Rebuild infrastructure
- Verify security

### The Business Impact

**For Different Industries:**

**Retailers (Walmart, Nordstrom):**
- Razor-thin margins ("air between my fingers")
- Costs continue, revenue stops
- 2 weeks down = catastrophic

**Entertainment (Sony Pictures):**
- Movie release schedules fixed
- Can't delay Julia Roberts film 18 days
- Promotions already spent
- Public loses interest

**Healthcare:**
- Lives at risk
- Regulatory consequences
- Patient care disrupted

---

## Gartner's Solution: Isolated Recovery Environment (IRE)

### Also Called "Vault"

**Origin:** Originally built for Sony Pictures to protect unreleased films

### The Five Requirements

#### 1. Isolated/Air-Gapped - MOST CRITICAL

**What it means:**
- Completely off network
- Physically disconnected
- "If you believe eventually defenses will be defeated, you've got to have isolated copy of data"

**How it works:**
- Network connects ONLY during scheduled replication
- Moves data
- Immediately disconnects
- Configurable frequency (once/day, twice/day, 86 times/day)

**Access method:**
- Physically walk to the system
- No remote access
- "You physically walk over to it. That's the only way."

#### 2. On-Premise

**Why:**
- Can't wait weeks to download from cloud
- Need data proximity
- Typically 1-hour restoration timeframe

**What it means:**
- Separate room on-site
- Unused hardware ready to go
- Pain to set up (rack, stack, install OS)
- But security over convenience

#### 3. Immutable

**Purpose:**
- Can't be altered after creation
- Critical for post-recovery lawsuits
- Audit trail preservation

**Note:** Still doesn't mean indestructible - just unmodifiable

#### 4. Zero-Trust

**Principles:**
- No assumptions about security
- Verify everything
- Multiple layers of authentication

#### 5. Full-Stack Solution

**Why:**
- Each API integration = increased attack surface
- Better: Single vendor (Dell, HPE) where everything works together
- One entry point to protect
- Then air-gap that entry point

---

## Recovery Process with Vault

### Data Scanning Requirements

#### Inbound Scanning (Required)
- **Tool:** Predator (or similar)
- **Time:** ~2 hours
- **Function:** Signature-based detection (like McAfee)
- **Limitation:** Only catches known threats

#### Outbound Scanning (Recommended Best Practice)
- **Time:** Another ~2 hours
- **Rationale:** Extra precaution
- **Note:** Seems redundant (no compute in clean room) but recommended anyway

### Active Directory Recovery

**Critical System:**
- Replicated every few seconds (0 seconds + network latency)
- Can recover in ~15 seconds for DR scenarios
- For cyber attacks: Restore to clean copy
  - Typically <3 hours old
  - Must be from BEFORE attack began

**Challenge:**
- Go back to "version of truth" about permissions
- "Who's really allowed to do what" or "who's who at the zoo"
- If 3 people hired during those 3 hours, HR needs to wait before onboarding

### Signature-Based Detection Limitations

**The McAfee Analogy:**
- Like old antivirus signatures
- Long list of 82 known attacks
- If signature database not updated, new malware slips through

**Quote:** "If McAfee didn't keep up [with new threats], you may actually believe that your archive is safe because Predator says there's nothing in there that I would know to watch for."

**Therefore:** Scan on way out too, just to be safe

---

## Industries Adopting Vault Solutions

### Early Adopters (Heavily Regulated)
- **Banking** - SEC requirements
- **Manufacturing** - Operational continuity
- **Government** - National security

### Rapidly Growing Adoption

#### Retail
- **Walmart:** Can't afford 6+ days down
- **Nordstrom:** Customers won't wait at register
- **Why:** Razor-thin margins, continuous costs

#### Entertainment
- **Sony Pictures:** Protect unreleased films
- **Why:** Fixed release schedules, massive marketing investments

#### Healthcare
- **Dual concern:** Money AND public safety
- **Why:** Patient lives, regulatory compliance

---

## Making the Business Case to Management

### The "Crying Wolf" Problem

**Scenario:** You've been warning them for years about:
- Network equipment needing replacement
- Storage being too slow
- Servers being too expensive

**Result:** They never listen. Why would they care about this?

### Three Proven Approaches

#### 1. Cybersecurity Insurance Premiums

**The Numbers:**
- Fortune 2000 companies: $10-15M/year
- Large enough to get audit committee's attention
- Increases after each incident (like car insurance)

**The Analogy:**
> "It's just like car insurance. You can't go out and get in a car accident every day for the next 2 years. Eventually your insurance premium will be $800 million."

**Key Point:** Unsustainable trajectory

#### 2. Calculate Hourly Downtime Cost

**Formula:**
```
Annual Revenue ÷ 8,760 hours = Hourly Cost of Downtime
```

> "Don't worry about getting it perfect. Get it wrong on purpose. That way they'll lean in and go 'Oh no, it's not $10 million an hour, it's $9.7 million an hour.' And you're like, 'Great, thanks for telling me that. By the way, can we afford that?'"

**Why This Works:**
- Gets them engaged in the calculation
- They correct you = they own the number
- Makes impact concrete and personal

#### 3. Public Safety & Legal Liability

**For Public Safety Organizations:**
- Harder to quantify than money
- But "when bodies start assuming room temperature because the computers aren't there, it generally gets attention"

**Personal Liability:**
- CIOs/CISOs carry E&O insurance (protects from financial liability)
- **BUT:** "If she goes to jail, doesn't matter how rich you are, it's gonna hurt"
- Can't insure against imprisonment

---

## Phone Cutover Analogy: The Importance of Preparation

### Mikes's Experience

**Approach:**
- Always did phone cutovers on Thursday 1:00 AM
- Why Thursday? One whole week to fix issues
- By Friday, most problems resolved
- If done right with mature environment: non-event

**Key Elements:**
- Comprehensive planning
- Practice runs
- Mature environment
- No technical debt
- No inertia

**Result:**
> "People pick up the phone, it works. They get their voicemail, everything's working. Some special things don't work, but you're conducting business."

### Application to Zero Trust / Disaster Recovery

**Same Principles:**
- Can't be slow in today's environment
- Need to move quickly but carefully
- Proper preparation = smooth execution
- Users don't even notice the change

**Modern Example:**
- Mike built entire remote endpoint access app in ONE WEEK from phone
- 158 iterations/commits
- Would have cost $100K+ 10 years ago
- Used platform called Revlet

**Lesson:** Speed matters, but preparation matters more

---

## Technical Best Practices

### Schedule-Based Security

**Simple but Effective:**
- Put schedules on firewall policies
- Don't want people accessing application midnight-6 AM? Close it.
- Form of zero trust
- Often overlooked

### Replication Frequency

**DR Solutions:**
- Journal-based (not snapshot)
- Every 0 seconds + network latency (typically ~5 seconds)
- Allows 10-15 second recovery times

**Cyber Vault:**
- Configurable based on risk tolerance
- Can be as frequent as every few seconds
- Typically 4-10 days retention (7 days is modal choice)

### Modern Use Case: Mobile Workspace

**Demonstration:**
- Samsung DeX phone setup
- AR glasses (Viture or Xreal brand)
- Keyboard and mouse
- Complete mobile workstation fits in small bag

**Why It Matters:**
- Future of work
- DR consideration: How do you support this?
- Can work anywhere with full capabilities
- Cheaper than traditional hardware

**Security Consideration:**
- How do you protect 100 users like this?
- Same security posture regardless of device
- Flexible edge in SASE framework

---

## Key Quotes & Takeaways

### On Traditional Security

> "Anything that's on a network, I'll find it. I'm not even that good anymore, but there's people that can attack anything that's on a network, period, the end."

### On Recovery Philosophy

> "There are companies that make stuff to keep bad guys out. There are a few of us that make stuff to help you recover when the bad guys get in anyway."

### On Business Case

> "In my opinion, it's money or it's public safety. When bodies start assuming room temperature because the computers aren't there, it generally gets attention."

### On Vendor Selection

> "Pick security over convenience. Anything other than [air-gapped isolated] is going to be vulnerable."

### On Testing

> "You gotta practice this stuff. These things don't happen at 2 o'clock in the afternoon Monday. They happen 2 o'clock in the morning on a Saturday."

---

## Implementation Recommendations

### Minimum Viable Protection

1. **Replicate more than once per day**
   - Unless you can afford to lose a day of business
   - Consider RPO (Recovery Point Objective)

2. **Have an isolated copy for recovery**
   - At minimum: isolated data
   - Ideal: isolated data + isolated hardware (clean room)

3. **Practice DR quarterly**
   - Test the process
   - Verify it works
   - Find gaps before you need it

### Progressive Adoption

**Don't try to do everything at once:**
- Start with most critical systems
- Build isolated recovery capability
- Expand coverage over time
- Balance cost vs. risk

### Testing & Validation

**Tabletop Exercises:**
- Include all stakeholders: CEO, CFO, CIO, Legal
- Practice "should we pay ransom?" conversation
- People get heated - good to work through beforehand
- Identify communication gaps

**Technical Testing:**
- Verify scan times
- Test recovery procedures
- Validate network air-gapping
- Confirm access controls

---

## The Bottom Line

### Assumptions to Operate Under

1. **Sophisticated attacks will eventually succeed**
   - Not if, but when
   - Defense in depth delays, doesn't prevent

2. **Traditional backups will be compromised**
   - Ransomware targets them first
   - Network connectivity = vulnerability

3. **Recovery speed determines survival**
   - 18-22 days too long for most organizations
   - Need faster path to restoration

4. **Isolation is the only true protection**
   - Air-gap from network
   - Physical separation
   - "Security over convenience"

### Success Criteria

**A successful vault implementation means:**
- Recovery measured in hours, not weeks
- Business continuity maintained
- Regulatory compliance achieved
- Insurance premiums manageable
- Leadership can sleep at night

**The Goal:**
> "When the generator comes on, and the power's out, you walk into your data center, generator's coming on, it's no fun though if there's no power and you paid $250,000 for infrastructure and you find out you're short on power and your battery/UPS is swapped incorrectly."

**Translation:** Prepare properly so recovery is a non-event, not a crisis.

---

## Additional Resources

- **Gartner:** Search "Isolated Recovery Environment" for latest research
- **Vendor Solutions:** HPE, Dell, others offer full-stack vault solutions
- **Testing Tools:** Predator, other signature-based scanning solutions
- **Best Practices:** Test quarterly, involve all stakeholders, balance speed with preparation

---

*These notes are my interpretations and summaries.*
