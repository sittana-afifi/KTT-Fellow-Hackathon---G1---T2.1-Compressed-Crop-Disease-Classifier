# 📈 Business Strategy: Project Hinga-AI

## 1. The Challenge: The Digital Last Mile
While our disease classifier is technically optimized (<10MB), two barriers prevent its adoption by the average Rwandan farmer:
* **Connectivity:** 4G/LTE coverage is inconsistent in deep rural districts.
* **Hardware:** Only a small percentage of smallholder farmers own smartphones capable of running image-based diagnostics.

## 2. Strategic Solution: "Human-in-the-Loop" Extension
We address this by deploying a **Village Lead (VL) Model** coupled with a **USSD Fallback** system.

### **The Workflow**
1. **The Diagnostic (High Tech):** Village Leads (trusted local youth or extension officers) use the smartphone app to perform field scans. The model runs **locally (Offline)** on their device.
2. **The Sync:** When the lead reaches a zone with connectivity, the diagnostic results (Disease Class + GPS + Farm ID) are uploaded to the central database.
3. **The Retrieval (Low Tech):** The individual farmer, regardless of their phone type, dials a shortcode (**`*123#`**) to view their farm's health status and treatment recommendations via SMS.

## 3. USSD Menu Structure (*123#)
Instead of data-heavy apps, farmers interact with the data via a zero-rated USSD menu:
* **Option 1: Farm Health Report** -> *"Your Maize scan from 24/04 shows signs of Rust. Recommendation: Apply [Product] and isolate the plot."*
* **Option 2: Treatment Marketplace** -> Direct link to purchase approved fertilizers/pesticides via Mobile Money.
* **Option 3: Agronomist Call-Back** -> Request a physical visit if the AI detection confidence was low.

## 4. Pilot Implementation & Unit Economics
**Location:** 50 Pilot Farms in the Musanze District.

| Item | Cost (RWF) | Frequency |
| :--- | :--- | :--- |
| **Agent Smartphone (Entry-level)** | 85,000 RWF | One-time |
| **USSD Session Cost** | 0 RWF | Zero-rated via Govt Partnership |
| **Agent Commission** | 500 RWF | Per successful farm scan |

**Sustainability:**
* **Revenue Model:** Subscription-based for Cooperatives or a small commission on treatment sales facilitated through the USSD menu.
* **Impact Goal:** Reduce crop loss due to Maize Blight/Rust by **25%** within the first harvest cycle.

## 5. Ethical Fairness & Reliability
* **Class Weighting:** The algorithm is tuned to prioritize diseases with high contagion rates (like Cassava Mosaic) to trigger early warnings for the whole village.
* **Human-in-the-Loop:** For any AI prediction with <70% confidence, the image is flagged for a remote agronomist to review before the SMS is sent to the farmer.
