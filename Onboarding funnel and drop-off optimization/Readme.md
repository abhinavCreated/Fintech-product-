# Onboarding Funnel & KYC Drop-Off Optimization

A product case study I built to dig into one of the biggest problems in fintech: getting a user from "just downloaded the app" to "actually funded their account."

## The problem

Most neobanks lose the majority of their users during KYC — the identity verification step. It's necessary (it's the law), but it's also where a huge chunk of people just... give up. I wanted to actually map that journey step by step and figure out where and why people drop off, instead of just assuming "KYC is annoying" and moving on.

## What I did

1. **Mapped the full onboarding journey** — 10 steps from app install all the way to a user's first funded transaction (sign-up, OTP, PAN entry, Aadhaar upload, liveness check, bank linking, etc.)
2. **Pulled a real customer dataset from Kaggle** and built a realistic funnel on top of it, using published industry benchmarks so the numbers aren't just made up
3. **Found the biggest leak**: only 13% of users make it all the way through, and the single worst step is Aadhaar document upload — over a third of eligible users drop off right there
4. **Dug into why**, not just where — turns out it's actually two separate problems: some users don't trust the app enough to hand over sensitive documents, and some users (especially older ones) just struggle with the technical steps like OTP and camera uploads
5. **Wrote a KYC policy** to handle both groups differently without weakening compliance
6. **Proposed and prioritized four fixes** (using a standard PM framework called RICE) and laid them out on a simple Now/Next/Later roadmap
7. **Packaged it all into a case study PDF** you'll find in this repo

## Key finding, if you only read one thing

Onboarding drop-off isn't one problem — it's two. A trust problem for people who already had a bad experience with the app, and a technical problem for people who struggle with the mechanics of KYC. Both hit hardest at the same step (document upload), which is why that step looks so broken.

## Tools used

Python (pandas, matplotlib) for the data work, spreadsheets for the funnel math, and plain old product thinking (RICE scoring, roadmapping) for turning the data into a plan.

## What's in this repo

- `Onboarding_KYC_Case_Study.pdf` — the full write-up, start to finish
- `onboarding_funnel_simulated.csv` — the working dataset
- `funnel_summary.csv` / `friction_segment_analysis.csv` — the numbers behind the charts
- `funnel_chart.png` / `friction_segment_chart.png` — the visuals
- `KYC_Policy_Proposal_Memo.md` and `Product_Improvements_Proposal.md` — the two supporting docs written along the way

## One honest note

The customer profiles in this project are real (from a public Kaggle dataset), but no company publicly shares actual step-by-step KYC drop-off data — that's commercially sensitive stuff. So I simulated the funnel behavior on top of the real customer data, using real industry benchmarks to keep it grounded. If this were a live product, the next step would be validating these patterns against real analytics tools like Mixpanel before acting on them. I'd rather be upfront about that than pretend this is live company data.
