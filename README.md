# Enterprise Rebate Management System (ERMS)

## The Origin
This started as a practical problem.

Rebates were being tracked through emails, random folders, inconsistent file names, and whatever system a contractor or project manager happened to use. Things slipped through—missed rebates, incomplete applications, no clear audit trail, and no real way to see total impact.

I took that over and built a structured spreadsheet and directory system to fix it. **That alone doubled the number of rebates captured at my campus.**

This project is the next step: turning that working system into something more durable and scalable across the university system.

---

## The Problem
The problem isn’t just messy data.

Across campuses, project managers are focused on construction. Rebates are small relative to total project cost, and often no one owns the process end-to-end.

So rebates—and the data behind them—simply disappear.

Not because people don’t care, but because there’s no system designed to carry them from start to finish.

---

## What this is trying to do
Connect the pieces of the rebate lifecycle into one flow:

- Project Planning  
- Rebate Commitments  
- Application Submission  
- Final Payment & Impact Recording  

So nothing gets lost between “this might qualify” and “this actually delivered value.”

---

## More Than a Check
When projects aren’t tracked properly, you lose visibility into long-term demand reduction and energy savings.

This system is meant to quantify that impact over a 10–20 year horizon—shifting the focus from a one-time check to long-term sustainability outcomes.

---

## How this repo is structured
This repo is an attempt to formalize what is currently a manual system. It’s not a finished product; it’s a working structure for thinking through the problem:

- **[Data Dictionary](./docs/data_model/Data_Dictionary.md)** → how projects, measures, and IDs are defined.
- **[Business Rules](./docs/data_model/Business_Rules.md)** → what the system should and shouldn’t allow.
- **Governance Logic** → how data stays auditable over time.

---

## Core ideas
- Track the full lifecycle (not just payments)  
- Treat rebates and savings like a pipeline (Identified → Committed → Verified)  
- Build structure early to avoid cleanup later  
- Reflect real-world complexity (multiple buildings, systems, IDs)  

---

## Future state
There are tools that can probably do 70–80% of this already.

But before choosing a tool, the process needs to be understood well enough to know what “good” looks like.

This project is an attempt to define that.

---

If you work in this space or see a better way to structure this, feel free to contribute.

---

**This didn’t start as a technical project. It started because things were disorganized and impact was getting lost. This is just an attempt to fix that in a way that lasts.**
