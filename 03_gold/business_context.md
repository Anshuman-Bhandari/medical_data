
## Who Is the Client Company?

The data belongs to **SafetyKleen** (or a very similar UK-based industrial services company). Here's what they do in plain English:

### The Business in One Line
> They **rent industrial cleaning machines** to businesses (garages, factories, workshops) and **service them regularly** — supplying chemicals, collecting waste, and maintaining equipment — all under **recurring service agreements**.

---

## 🔧 What Does This Company Actually Do?

Imagine you own a car garage. Your mechanics need to clean greasy engine parts. You can't just wash them with soap — you need specialized **parts washing machines** that use industrial solvents or aqueous (water-based) cleaning solutions.

**SafetyKleen's business model:**

```
┌─────────────────────────────────────────────────────┐
│              HOW THE BUSINESS WORKS                  │
├─────────────────────────────────────────────────────┤
│                                                      │
│  1. PLACE a cleaning machine at customer's site      │
│  2. SUPPLY the chemical/solvent it needs             │
│  3. VISIT regularly to service the machine           │
│  4. COLLECT the used/waste chemicals                 │
│  5. BILL monthly under a service agreement           │
│  6. REPEAT every service interval (e.g., 13 weeks)  │
│                                                      │
│  Revenue = Recurring monthly fees × thousands of     │
│            customers × multiple agreements each      │
└─────────────────────────────────────────────────────┘
```

### Their Product Lines (from the data)

| Line of Business | What It Means | Example from Data |
|---|---|---|
| **Machine Services** (221,770 rows) | The core — cleaning machines placed at customer sites | Solvent Parts Cleaners, Aqueous Units, Spray Equipment Cleaners, Ultrasonic cleaners |
| **Auto Waste** (128,797 rows) | Collecting waste oil, solvents, and chemicals from customers | Oil Filters, Oil Collector Fees |
| **Oil** (14,293 rows) | Used oil collection and recycling | Oil collection services |
| **Chemistry** (11,457 rows) | Supplying industrial cleaning chemicals | KLEEN7960S, Natural Solvent, Resinpro |
| **Allied** (446 rows) | Other related products | Wipes, Document Fees |

### Their Customers

- **B2B only** — businesses, not consumers
- Mostly in the **United Kingdom**
- Range from tiny 1-9 employee workshops to **1000+ employee** large enterprises
- Industries: automotive garages, manufacturing plants, engineering workshops, facilities management
- Tiered system: **Platinum+** → **Platinum** → **Diamond** → **Key Account**

---

## 💰 How Do They Make Money?

This is a **recurring revenue / subscription-like business**:

```
Customer signs an AGREEMENT
  → Company places MACHINE(S) at the site
    → Company visits every X weeks to SERVICE
      → Customer gets BILLED monthly
        → Agreement AUTO-RENEWS unless cancelled
```

### Key Financial Terms from the Data

| Term | Meaning |
|---|---|
| **VAN** (Value of Annual Net) | Annual revenue from a customer/agreement — **the money at stake** |
| **BoB** (Book of Business) | Total portfolio value — what a customer is worth |
| **product_bob** | Revenue from the product/machine rental |
| **fee_bob** | Revenue from service fees |
| **total_bob** | product_bob + fee_bob = total agreement value |
| **unit_amount** | Price per unit/service visit |

### Revenue Numbers at a Glance
- Average **VAN per agreement**: ~£3,800/year
- Average **BoB per customer**: ~£28,000 (total across all their agreements)
- A large customer (multiple machines, agreements) can be worth **£100K–£3.8M** annually
- **376,803 active product lines** across **23,772 customers** — massive recurring revenue base

---

## ⚠️ The Business Problem: CHURN

### What Is Churn Here?

Churn = **a customer wanting to leave** (cancel their service agreement).

This is NOT like Netflix where someone clicks "cancel." In B2B industrial services, churn is a **process**:

```
┌──────────────────────────────────────────────────────────┐
│                    THE CHURN LIFECYCLE                     │
├──────────────────────────────────────────────────────────┤
│                                                           │
│  TRIGGER                                                  │
│  ├── Customer calls to cancel ("Notice in Writing")       │
│  ├── Account Manager spots a risk ("Proactive")           │
│  ├── Credit Controller flags debt ("Aged Debt")           │
│  └── Service issue reported ("Complaint Case")            │
│                                                           │
│  A RETENTION CASE is created                              │
│  ├── Case Type: "Risk" (early warning) or                 │
│  │              "Cancellation" (formal request)           │
│  │                                                        │
│  ├── Risk Types:                                          │
│  │   • Contract Expiring Soon                             │
│  │   • Competitor Activity                                │
│  │   • Customer Unsatisfied                               │
│  │   • Machine Not Being Used                             │
│  │   • Debt                                               │
│  │   • Site Access issues                                 │
│  │                                                        │
│  RESOLUTION                                               │
│  ├── ✅ "Customer Saved" (37,477 cases) — RETAINED        │
│  ├── ❌ "Customer Lost" (24,519 cases) — CHURNED          │
│  ├── 🔄 "Converted to Cancellation" (9,887) — escalated  │
│  └── ⏳ "OPEN - In Progress" (13,451) — still fighting    │
│                                                           │
└──────────────────────────────────────────────────────────┘
```

### Two Levels of Churn

| Level | Definition | What It Means |
|---|---|---|
| **Agreement-Level Churn** | `Resolution Status = "Customer Lost"` for a specific case/agreement | Customer cancelled ONE agreement (maybe one machine out of three) |
| **Customer-Level Churn** | ALL agreements for that customer are lost | Customer completely left — **total relationship lost** |

> **Example**: A factory has 3 cleaning machines from SafetyKleen (3 agreements). If they cancel 1 machine → agreement-level churn. If they cancel ALL 3 → full customer churn.

### Pull Types

| Pull Type | Meaning |
|---|---|
| **Full Pull** (46,305 cases) | Customer wants to remove ALL machines — complete exit |
| **Partial Pull** (3,899 cases) | Customer wants to remove SOME machines — downsizing |

---

## 🎯 Why Does JMAN Care About This?

JMAN Group is a **data consultancy for private equity firms**. Here's the business logic chain:

```
Private Equity firm owns SafetyKleen (or similar company)
  → They want to GROW the company's value
    → Churn DESTROYS recurring revenue
      → JMAN is hired to use data science to PREDICT and PREVENT churn
        → That's YOUR project
```

### The Money at Stake

From the data:
- **24,519 cases** resulted in "Customer Lost"
- Average VAN of lost customers: **£2,860/year**
- Estimated annual revenue lost to churn: **~£70M+ per year**
- If you can predict churn early and save even **10% of those customers**, that's **£7M+ saved annually**

### Why Prediction Matters

| Without Prediction | With Prediction |
|---|---|
| React AFTER customer calls to cancel | Identify at-risk customers BEFORE they call |
| Expensive last-minute negotiations | Proactive outreach while relationship is still good |
| Account managers spread thin across all customers | Focus retention efforts on the most likely churners |
| Don't know which customers are highest risk | Prioritize by churn probability × revenue at risk |

---

## 📊 The Two Datasets Explained

### 1. Retention.csv — "The Churn Cases"
This is the **retention/cancellation case management system**. Every time there's a risk of losing a customer, a case is created.

| Column | Business Meaning |
|---|---|
| **Case ID** | Unique identifier for each retention case |
| **Case Title** | The REASON for the risk (e.g., "Competitor better value", "Site Closure", "Machine not used") |
| **VAN** | Annual revenue at stake for this case |
| **Pull VAN / New VAN** | Revenue pulled out vs. new revenue negotiated |
| **Number of Contracts** | How many agreements this customer has |
| **Machines** | How many machines at the customer site |
| **Case Type** | Risk (early warning) vs. Cancellation (formal request) vs. Price Increase |
| **Risk** | Specific risk category (Competitor Activity, Debt, etc.) |
| **Resolution Status** | **THE TARGET** — Customer Saved vs. Customer Lost |
| **Case Origin** | How we found out (proactive vs. reactive) |
| **CompanySize / Customer Tier** | Customer profile information |
| **Dates** | Timeline of the retention case |

### 2. BoB.xlsx — "The Book of Business"
This is the **complete product/service portfolio** — every agreement, every machine, every chemical for every customer.

| Column | Business Meaning |
|---|---|
| **account_number** | Customer identifier (links to Retention) |
| **agreement_number** | Specific service agreement |
| **line_of_business** | Machine Services, Auto Waste, Oil, Chemistry |
| **total_bob / product_bob / fee_bob** | Revenue from this agreement line |
| **machine / machine_variant** | Which machine model is placed at the site |
| **chemistry** | Which cleaning chemical is being used |
| **service_interval** | How often (in weeks) the machine is serviced |
| **renewal_type** | Auto-renew or manual renewal |
| **system_status** | Active, Estimated, Canceled, Expired |

---

## 🧠 What Your Model Should Ultimately Answer

> **"Given what we know about a customer — their size, tier, revenue, machines, service history, complaints, and product portfolio — how likely are they to churn?"**

### Business Questions the Model Should Help Answer:

1. **Which customers are most likely to churn in the next 3-6 months?**
2. **What are the top drivers of churn?** (Price? Service quality? Machine usage? Debt?)
3. **How much revenue is at risk?** (VAN × churn probability)
4. **Which customer segments are highest risk?** (Small companies? Certain industries?)
5. **Are proactive interventions working?** (Cases from "Account Manager" vs. "Notice in Writing")
6. **Does product diversity protect against churn?** (More products = harder to leave?)

---

## 🔑 Key Business Insights Already Visible

From the data exploration:

| Insight | Evidence | Business Implication |
|---|---|---|
| **Saved customers have HIGHER VAN** | Saved avg: £5,089 vs. Lost avg: £2,860 | Company fights harder to keep valuable customers |
| **~31% agreement-level churn rate** | 15,051 lost out of 48,887 cases | Significant — nearly 1 in 3 at-risk agreements is lost |
| **"Risk" cases convert to cancellation 20% of the time** | Risk → Converted to Cancellation = 20.4% | Early warning system exists but doesn't always prevent loss |
| **Most revenue is from Machine Services + Auto Waste** | 93% of BoB rows | Core business is machine-based recurring services |
| **99.5% agreements are auto-renewal** | 374,758 out of 376,784 | Non-auto-renewal agreements are rare — worth flagging as risk |
| **Company size matters** | Large spread across segments | Smaller companies may be harder to retain (less switching cost) |

---

> [!TIP]
> **Think of it this way**: This company is like a "Netflix for industrial cleaning machines." Customers subscribe, get machines placed at their site, get regular servicing, and pay monthly. Your job is to predict who's about to "unsubscribe" and why — so the company can intervene before they leave.
