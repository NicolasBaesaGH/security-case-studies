# OSINT Case Study: Tracing a Facebook Marketplace Scam Network

**Type:** Phone number trace & scam pattern investigation
**Region:** Philippines
**Tools/Techniques:** TrueCaller lookup, Google dorking, Facebook OSINT, phishing domain analysis, courier invoice forensics, geolocation inference
**Status:** Findings reported to platform/authorities; case anonymized below for public writeup

---

## 1. Overview

This case study documents an open-source intelligence (OSINT) investigation into a phone number flagged across multiple independent public sources as being tied to a **Facebook Marketplace "scam seller" scheme**. The goal was to determine whether the number was part of a known fraud pattern, corroborate it across sources, and assess how much could be learned using only publicly available tools.

> **Note on redaction:** All personally identifying details (full name, date of birth, home address, and ID document images) referenced in the original investigation have been removed or generalized in this writeup. The individual identified in source material has not been independently verified as the actual operator of the account, and publishing unverified identity claims tied to fraud accusations is not something I do — even when the underlying pattern-matching is solid. This piece focuses on the **methodology**, not the identification.

## 2. The Reported Scam Pattern

Investigation began from a single mobile number reported on Reddit (r/ScammersPH). Cross-referencing that number against Facebook groups and search engines revealed a consistent, repeatable scam pattern:

![Marketplace scam flow diagram](./scam-flow-diagram.svg)

1. Seller lists an item on Facebook Marketplace.
2. Seller arranges a video call showing the item, a receipt, and an ID to build trust.
3. Seller sets up a **fake courier tracking link** mimicking a legitimate delivery service.
4. Once the buyer sends full payment, the seller blocks them.

This pattern recurred across multiple unrelated complaint threads — a strong signal that the number belonged to an active, repeat-use scam operation rather than a one-off dispute.

## 3. Methodology

### 3.1 Reverse Number Lookup
Ran the subject number through TrueCaller. No registered name was returned, but carrier (Globe Telecom) and country were confirmed — useful for narrowing scope and ruling out spoofed/VOIP numbers.

### 3.2 Google Dorking
Used `site:facebook.com` search restrictions against both the subject number and a linked alternative number found in later steps. This surfaced additional, independent complaint posts not linked to each other — a key corroboration technique, since it shows the number recurring across unconnected victims rather than a single source.

### 3.3 Courier Invoice Forensics
A photographed courier invoice (used by the seller as "proof of shipment") included a branch phone number with a **"047" area code** — inconsistent with the claimed branch location. Cross-checking the area code against the courier's internal branch origin code corroborated a likely **Central Luzon** operating region, rather than the location implied by the invoice's letterhead. This is a good example of how metadata *inside* a document (routing codes, area codes) can contradict the story the document is trying to tell.

### 3.4 Phishing Infrastructure
The scheme relied on a **fake courier tracking page** hosted on a look-alike domain, designed to visually mimic the real delivery service's tracking UI and convince the buyer a courier was genuinely en route. Identifying and documenting this domain allows it to be reported to the platform and to Google Safe Browsing.

### 3.5 Cross-Source Correlation
Combined all of the above into a single evidence chain:
- Subject number ↔ alternative number (co-occurring on the same invoice and in the same complaint threads)
- Both numbers ↔ recurring pattern across multiple, independently-posted community warnings
- Invoice metadata ↔ geographic inference independent of any name or profile claim

## 4. Findings Summary

| Finding | Corroboration |
|---|---|
| Number tied to active scam pattern | 3+ independent community reports, consistent methodology described in each |
| Alternative number identified | Recurs on physical invoice and separate Facebook threads |
| Likely operating region | Area code + courier internal routing code agree |
| Phishing domain in active use | Screenshot evidence, mimics real courier tracking UI |

## 5. Recommendations Produced for the Client

- Do not engage the number(s) directly beyond what's needed for reporting.
- Report number(s) and associated profile(s) to the platform and to PNP-ACG / NBI Cybercrime Division.
- Report the phishing domain to the courier company and Google Safe Browsing.
- Treat any name/ID imagery surfaced in community posts as **unverified** — identity documents can be stolen, fabricated, or borrowed, and should never be the sole basis for public accusation.

## 6. Skills Demonstrated

- Multi-source OSINT correlation (Reddit, Facebook, search engines, reverse-lookup tools)
- Reading metadata/routing information out of scanned documents to catch inconsistencies
- Identifying and safely documenting phishing infrastructure
- Structuring findings into a clear, actionable report for a non-technical client
- **Responsible handling of unverified identity claims** — knowing when *not* to publish something, even when it's compelling

---

*This writeup is a generalized case study based on real investigative work. Identifying details have been redacted to protect an unverified individual and to comply with responsible disclosure practices.*
