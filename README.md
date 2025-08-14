# 🛍️ E-Commerce Customer Segmentation — CSCN 8000

**Course:** Artificial Intelligence Algorithms & Mathematics  
**Assignment:** Customer Segmentation for E-commerce Personalization  
**Notebook:** `erisScript.ipynb`  

---

## 🎯 Overview
This project clusters customers by real behavior (views, carts, purchases) to enable **personalized marketing**.  
Pipeline: load raw logs → clean → build **customer-level** features → scale & **PCA** → **K-Means** → interpret segments → marketing actions.

---

## 📂 Dataset
**Source:** Kaggle — *E-commerce Customer Behavior*  
**Columns:** `event_time`, `event_type`, `product_id`, `category_id`, `category_code`, `brand`, `price`, `user_id`, `user_session`.

---

## 🚀 How to Run
1. Put the Kaggle CSVs **in the same folder** as the notebook.  
2. Open `erisScript.ipynb` and run cells **top → bottom**.  
3. Artifacts saved:  
   - `customer_segments.csv` — `user_id` → cluster  
   - `segment_summary.csv` — per-cluster medians & user counts

---

## 🧭 Method (Pipeline)
1. **Load & Explore** 🔍  
   Concatenate monthly CSVs → single DataFrame; parse `event_time`; sort; show event counts & distribution.
2. **Preprocess & Feature Engineering** 🧹  
   - Missing values: fill `category_code`/`brand` with `"unknown"`; drop rows missing `user_id` or `event_time`.  
   - Aggregate **per user**:
     - Volume: `total_events`, `n_view`, `n_cart`, `n_purchase`, `n_sessions`  
     - Variety: `unique_products`, `unique_categories`, `unique_brands`  
     - Monetary: `revenue`, `avg_price_purchased`  
     - Funnel: `conversion_rate`, `view_to_cart_rate`, `cart_to_purchase_rate`  
     - Temporal: `recency_days`, `tenure_days`
3. **EDA** 📊  
   Bar charts: **event types** and **top categories**; note browser/abandoner/loyalist patterns.
4. **Feature Transformation** 🔧  
   `StandardScaler` (zero-mean, unit-var). `PCA(n=2)` for denoising & visualization (report explained variance).
5. **Model Selection & Clustering** 🧩  
   Choose **k** via **silhouette score** for `k ∈ {3…7}`; fit **K-Means** on scaled features; visualize clusters in PCA(2).
6. **Interpretation & Marketing** 🧠  
   Summarize cluster medians & sizes; label segments; propose targeted actions; save CSVs.

---

## 📈 Key Results (this run)
- **Events:** 109,950,743 total  
  - view **94.89%** (104,335,509) · cart **3.60%** (3,955,446) · purchase **1.51%** (1,659,788)
- **Chosen k:** **3** (highest silhouette in tested range)  
- **Users segmented:** **5,316,649**
  - **Cluster 0 — Browsers / One-time Visitors (86.99%)** 🕵️‍♀️  
    - Low activity, 0 purchases; recency ≈ 19d → **onboarding & first-purchase incentives**
  - **Cluster 1 — High-Value Loyalists (6.22%)** 💎  
    - Purchases ≈ 2 (median), revenue ≈ **$531.29**, avg price ≈ **$272.31** → **VIP perks, bundles, replenishment**
  - **Cluster 2 — Heavy Researchers (6.79%)** 🔬  
    - Many views, broad category exploration, few/no purchases → **price-drop alerts, reviews, checkout nudges**

---

## 💡 Personalization Playbook (examples)
- **Loyalists:** 🎁 VIP program, early access, replenishment reminders, premium bundles.  
- **Browsers:** 📚 Buying guides, social proof, welcome series, first-purchase promo.  
- **Cart-shy / Researchers:** ⏰ Cart reminders, 🚚 free-shipping thresholds, 🧾 price-drop alerts, simplified checkout.  
- **Category Specialists:** 🧷 Deep category recs, complementary bundles, adjacent-category cross-sell.

---

## ✅ Notebook ↔ Assignment Mapping
- **Task 1:** Loading + event counts/distribution (code + markdown)  
- **Task 2:** Missingness handling + customer features (counts, monetary, funnel, temporal)  
- **Task 3:** EDA plots + observations  
- **Task 4:** Scaling rationale + PCA variance & scatter  
- **Task 5:** k-selection by silhouette + K-Means + PCA visualization  
- **Task 6:** Segment characteristics + marketing insights; CSV exports

---

## ⚠️ Limitations & Next Steps
- K-Means assumes roughly spherical clusters (Euclidean).  
- Large “unknown” categories can dilute category insights.  
- Next: try **HDBSCAN** for irregular shapes; per-cluster **top-category** tables; add **temporal segmentation** (seasonality); run **uplift tests** per segment.

---

## 🧰 Environment
Python 3.x · `pandas` · `numpy` · `matplotlib` · `scikit-learn`

