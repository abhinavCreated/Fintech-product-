# PM Proposal Memo: Risk-Based KYC Policy for Onboarding

**To:** Head of Product, Compliance Lead, Engineering Lead
**From:** [Your Name], Product Manager
**Date:** [Date]
**Re:** Proposed risk-based KYC policy to address onboarding drop-off

---

## 1. Why This Memo Exists

We are converting only **13% of installs into a funded transaction**. Of every 10,000 users who download the app, roughly 8,700 never fund an account. The single largest leak is **Aadhaar Document Upload, where 38.5% of eligible users drop off** — nearly 3x the rate of any other stage in the funnel.

This memo proposes a KYC policy that treats onboarding not as one uniform process, but as a **risk-based, segment-aware process** — because the data shows we are not losing one type of user for one reason. We are losing two different types of users for two different reasons, and our current one-size-fits-all KYC flow serves neither well.

---

## 2. The Problem, In Numbers

| Finding | Data |
|---|---|
| Overall funnel conversion | 13.0% (Install → Funded) |
| Worst single stage | Aadhaar Document Upload — 38.5% drop-off |
| Users with a prior complaint | Drop off at **54.6%** at Aadhaar Upload (vs. 36.1% baseline) and complete the funnel at only **3.8%** |
| Users aged 56+ | Drop off at **19.1%** at OTP Verification (vs. 9.6% for 18–25) — more than double |
| Low-satisfaction users | Complete the funnel at **8.9%** vs. 15.9% for mid-satisfaction users |
| Metro Tier (geography) | No meaningful difference (~13% across all tiers) — ruled out as a driver |

**Read together, these numbers point to two distinct root causes:**

- **A Trust Barrier** — users who already have low confidence in us (prior complaints, low satisfaction) hesitate or abandon specifically at the moments we ask for sensitive identity documents (PAN, Aadhaar, Bank Link). This is a *psychological* cost, not a technical one.
- **A Technical Barrier** — older users disproportionately fail at mechanically demanding steps (OTP entry, camera-based document upload, liveness/selfie checks). This is a *usability* cost, not a trust one.

Aadhaar Upload is where both barriers hit simultaneously — it's sensitive (trust) *and* camera/file-dependent (technical) — which is exactly why it's our worst stage by a wide margin.

---

## 3. Why This Matters (Business Impact)

- **CAC is being wasted at scale.** Every user we acquire and then lose during KYC represents fully-spent acquisition cost with zero return. At 87% pre-funding drop-off, we are effectively paying full CAC for a completed customer roughly 1 in 8 times.
- **Trust erosion compounds.** Users who abandon during a failed KYC attempt are unlikely to be neutral — a failed, confusing, or invasive-feeling onboarding experience is a plausible source of the *next* complaint, feeding the same cycle we're trying to break.
- **Regulatory exposure runs in the opposite direction of user experience if handled naively.** KYC/AML obligations under the RBI's Master Direction on KYC, the Prevention of Money Laundering Act (PMLA), and Aadhaar Act requirements are non-negotiable — we cannot simply "make KYC easier" by cutting steps. Any policy proposed here has to reduce *friction*, not reduce *rigor*.
- **A segment we're currently underserving (56+) represents real deposit potential.** Older users tend to carry higher average balances in traditional banking; losing them disproportionately at OTP/technical steps is a growth opportunity being left on the table, not just a support cost.

---

## 4. Proposed Policy: Risk-Based, Segment-Aware KYC

Rather than one identical KYC flow for all users, this policy proposes **three coordinated tracks**, applied at the point a user enters onboarding:

### Track A — Trust-Sensitive Users
*(Triggers: prior complaint on file, low satisfaction score, or first-time interaction with a sensitive-data request)*

- Before requesting PAN/Aadhaar, insert a **short, plain-language trust message**: what data is collected, why, how it's secured, and a link to a human support option — reducing the "why do you need this" hesitation directly at the point of highest anxiety.
- Route these users to **priority human support** if they pause more than 60 seconds on the PAN or Aadhaar screen, rather than letting them silently exit.
- Do **not** reduce the verification rigor for this group — the intervention is entirely about *communication and reassurance*, not about lowering compliance standards.

### Track B — Technical-Risk Users
*(Triggers: age 56+, or two or more failed OTP/upload attempts)*

- Offer **assisted verification**: larger UI text, an option to switch to a guided video call for document capture instead of self-serve camera upload, and OTP fallback via voice call if SMS fails twice.
- This aligns with RBI's existing **Video-based Customer Identification Process (V-CIP)** provisions, meaning this isn't a new compliance category — it's applying an already-approved verification method to the users who need it most.

### Track C — Standard Users
*(Everyone else — the majority, currently converting reasonably)*

- Keep the current self-serve flow as-is. **Do not add friction here** — over-applying "trust building" messaging or "assisted" flows to users who don't need it will slow down our best-converting segment for no benefit.

### Governance Baseline (applies to all tracks)
- All KYC decisions remain logged and auditable per PMLA/RBI recordkeeping requirements, regardless of track.
- Risk scoring (which track a user is routed to) is re-evaluated, not one-time — a Track A user who completes onboarding successfully doesn't stay flagged indefinitely.
- Central KYC Registry (CKYCR) checks apply uniformly across all three tracks; no track bypasses regulatory identity verification, only the *presentation and support layer* changes.

---

## 5. Expected Impact

Directionally, based on the segment gaps observed:

- If Track A messaging closes even half the gap between complaint-users' Aadhaar drop-off (54.6%) and the baseline (36.1%), that alone recovers a meaningful share of ~2,000 at-risk users per 10,000 installs.
- If Track B assisted verification brings the 56+ OTP drop-off (19.1%) down toward the 18–25 baseline (9.6%), we protect a segment that is small in volume but disproportionately valuable in deposit size.
- Neither change touches Track C, so we're not risking our currently-healthy majority conversion path while we fix the two specific leaks.

This should be validated with a **phased A/B rollout** (Track A and B messaging/flows tested against current flow) before full deployment — see Risks below.

---

## 6. Risks & Trade-offs

- **Speed vs. Risk:** Assisted/video-based verification (Track B) is slower per user than self-serve upload. This is an intentional trade — we accept added handling time for a segment we're currently losing outright.
- **False positives in routing:** Segment triggers (age, complaint history) are proxies, not certainties. Recommend the routing logic be reversible — a user can always request the standard flow if they don't want the assisted path.
- **Compliance-first, always.** No part of this proposal reduces document verification standards, retention requirements, or audit logging. Every change here is UX/communication-layer, sitting on top of an unchanged compliance floor.

---

## 7. Next Steps

1. Confirm Track A/B trigger thresholds with Compliance (satisfaction score cutoff, complaint lookback window, age threshold).
2. Scope Track B's video-KYC assisted flow with Engineering — estimate build effort against V-CIP-compliant vendor options.
3. Design Track A trust-messaging screens with UX (Figma) — target: no added steps, just clearer framing at existing steps.
4. Define A/B test success metric: Aadhaar Upload stage conversion rate, segmented by track, measured over a 2–4 week pilot.
