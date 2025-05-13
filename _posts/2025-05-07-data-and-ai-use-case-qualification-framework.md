---
title: How to qualify and prioritise your Data and AI use cases 
date: 2025-05-07 00:34:00 +0800 
categories: [Data and AI Strategy]
tags: [Data, AI, Strategy]
---

# How to gather, qualify and prioritise the Data and AI use cases?

As soon as you start defining your Data and AI strategy, organization will need to start gathering use cases. As strategy only as good as its execution, and to start reap benefit on your investment in definining the Data/AI strategy, organization will start break down the strategy and collect multiple use cases

As organisations race to become more data-driven and AI-enabled, it's common to see teams overwhelmed with ideas, proofs of concept, and a growing backlog of use cases. But how do you know which use cases are worth pursuing—and which ones are likely to fail or drain resources?

To address this challenge, organization need a clear, structured way to evaluate the business impact, feasibility, and readiness of each use case. In this post, We will walk through a simple yet robust **Data and AI Use Case Qualification Framework** that helps teams make smarter decisions.

---

## 1. Business Value

The first—and arguably most important—dimension is **business value**. This is where we ask: _Why does this use case matter?_

Key criteria to assess:
- **Revenue Impact**: Will it help increase sales or open new revenue streams?
- **Cost Savings**: Can it reduce manual effort, operational inefficiencies, or compliance overhead?
- **Customer/Employee Experience**: Will it enhance user satisfaction, personalization, or speed?
- **Strategic Alignment**: Does it support business objectives or provide a competitive edge?

> 🔍 Score each use case from 1 (low value) to 5 (high value).

---

## 2. Data Readiness

AI is only as good as the data that fuels it. A high-value use case may stall without the right data.

Key questions to consider:
- **Is the data available and accessible?**
- **Is the data clean, consistent, and reliable?**
- **Do we have enough volume and variety of data?**
- **Do we have labeled data if the model needs supervision?**

> 📊 Score from 1 (data unavailable or poor quality) to 5 (data is rich and ready).

---

## 3. Technical Feasibility

Not all problems are technically solvable today—at least not easily. It's essential to evaluate how feasible the use case is from a technology perspective.

Look at:
- **Model Complexity**: Is this a mature problem space (e.g., forecasting) or something cutting-edge (e.g., generative AI for legal text)?
- **Systems Integration**: Can the solution plug into existing workflows and platforms?
- **Latency Requirements**: Do predictions need to happen in real time?
- **Tooling Availability**: Do we already have the tools and MLOps pipelines in place?

> 💡 Score from 1 (high complexity, low readiness) to 5 (simple to implement).

---

## 4. Organisational Readiness

Many AI projects fail not due to technical issues—but because the organisation isn't ready for change.

Key factors:
- **Stakeholder Buy-in**: Are business and IT sponsors aligned and supportive?
- **Change Management**: Will the users adopt and trust the AI outputs?
- **AI Literacy**: Do teams understand how to use or interpret AI results?
- **Skillsets**: Do we have the right talent in place (e.g., data scientists, engineers)?

> 🏢 Score from 1 (no support or skills) to 5 (high alignment and readiness).

---

## 5. Risk & Compliance

Finally, we must assess whether the use case introduces unacceptable risk, especially in regulated industries.

Consider:
- **Data Privacy & Security**: Are we handling sensitive data?
- **Bias & Fairness**: Could the model produce unethical or unfair outcomes?
- **Regulatory Constraints**: Are there laws or standards to comply with (e.g., GDPR, HIPAA)?
- **Explainability Requirements**: Do we need to justify predictions to end users or regulators?

> ⚠️ Lower scores = higher risk. Score from 1 (high risk) to 5 (low risk).

---

## Bringing it all together: The Prioritisation Matrix

Once you’ve scored each use case across these five dimensions, you can calculate a total score and plot it on a **2x2 prioritisation matrix**:

| Value / Feasibility | Low Feasibility        | High Feasibility          |
| ------------------- | ---------------------- | ------------------------- |
| **High Value**      | Invest in capabilities | Prioritise immediately    |
| **Low Value**       | Avoid or defer         | Quick wins / nice to have |

This approach allows teams to:
- Focus resources on high-impact, feasible use cases
- Identify gaps in data, tools, or org readiness
- Build a roadmap that aligns with business priorities


## How should we start in gathering use cases?
There are a total of 4 approaches:
1. Strategy-Led (Top-Down)
Start from business strategy and goals.

Understand key strategic priorities (e.g., growth, cost reduction, risk management).

Identify where data/AI can accelerate or enable those goals (e.g., customer churn prediction, revenue forecasting).

Strength: High alignment with leadership and business value.
Use When: Starting from executive vision or digital transformation plans.

2. Value Chain & Process-Led (Business-Driven Discovery)
Start from the value chain, then zoom into core business processes.

Map the end-to-end value chain (e.g., sourcing → production → sales → service).

Prioritize high-impact areas, then analyze key processes within.

Identify inefficiencies, decision points, or automation opportunities for data/AI intervention.

Strength: Grounded in how the business operates, with clear tactical and strategic use cases.
Use When: Engaging operational leaders or conducting broad discovery workshops.

3. Data-Led (Bottom-Up)
Start from available data assets.

Explore data repositories to uncover patterns, trends, anomalies.

Use exploratory analysis, clustering, or data profiling to spot untapped opportunities.

Strength: Fast prototyping and reveals insights not visible through business lens.
Use When: You have strong data assets and analytics capabilities but unclear business asks.

4. Capability-Led (Technology Push)
Start from new technology capabilities (e.g., LLMs, computer vision, real-time analytics).

Brainstorm innovative applications that the business hasn't yet considered.

Match capabilities to latent business needs or create new user experiences.

Strength: Drives innovation and differentiation.
Use When: Exploring disruptive ideas, engaging innovation labs, or responding to competitor moves.

---
## 📌 What Should You Record in Your Data & AI Use Cases?

Bernard Marr has shared some excellent reference materials that provide a strong foundation for defining AI and data use cases:

- [AI Use Case Template](https://bernardmarr.com/how-to-define-your-ai-artificial-intelligence-use-cases-with-handy-template/)
- [Data Use Case Template](https://bernardmarr.com/how-to-define-a-data-use-case-with-handy-template/)

These templates cover key elements such as business objectives, stakeholders, data sources, and success measures. However, one important enhancement worth considering is the **inclusion of estimated cost and potential ROI**.

### 🎯 Why ROI Should Be Included

Clearly articulating **expected ROI** strengthens the business case for a use case, especially when aligned to:

- **Top-line impact**: e.g., revenue growth, increased market share
- **Bottom-line impact**: e.g., cost reduction, improved operational efficiency
- **Risk mitigation**: e.g., enhanced compliance, reduced fraud or error

While risk-related use cases may not directly drive revenue or cost savings, they can still be **quantified in financial terms**. For example:

> Under IFRS and GAAP accounting standards, significant business risks—such as compliance violations or operational disruptions—may require financial provisions in the P&L. This gives you a mechanism to tie risk mitigation efforts to quantifiable financial outcomes.

### ✅ Recommendation

For high-impact or strategic use cases, consider adding the following fields to your documentation:

- **Estimated implementation cost** (licensing, infrastructure, resources)
- **Expected financial impact** (e.g., projected savings, revenue uplift)
- **ROI estimate** (based on leadership-aligned metrics like net profit, gross margin, or risk-adjusted benefit)

Engaging senior stakeholders early to align on these metrics can significantly improve prioritization and sponsorship of your data and AI initiatives.

---

## Final Thoughts

Gathering, Qualifying and prioritising Data and AI use cases is critical for turning hype into real value. With a structured framework, you can reduce wasted effort, build stakeholder trust, and scale AI initiatives more effectively.

Whether you're just starting out or looking to refine your existing use case pipeline, this framework gives you a practical foundation to move from idea to impact.

