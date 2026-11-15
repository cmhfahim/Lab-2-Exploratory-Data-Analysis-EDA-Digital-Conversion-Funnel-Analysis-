# Exploratory Data Analysis (EDA) & Digital Conversion Funnel Analysis 

A reproducible Python workflow for digital telemetry analysis. This project generates 5,000 synthetic Google Analytics 4 (GA4)-style user sessions, performs data cleaning and exploratory analysis, constructs a multi-step conversion funnel, and evaluates behavioral correlations to pinpoint primary conversion blockers.

---

## Key Findings

* **Primary Conversion Blocker:** The largest drop-off occurs between **Session Start** and **Add to Cart**, where **70.60%** of sessions (3,530 users) exit without adding an item.
* **Cart-to-Purchase Retention:** Once users add an item to their cart, **61.56%** complete a purchase, while **38.44%** abandon checkout.
* **Overall Conversion Rate:** **18.10%** of total sessions result in a completed purchase (905 out of 5,000 sessions).
* **Device Consistency:** Conversion rates remain consistent across desktop (**18.61%**), tablet (**17.58%**), and mobile (**17.57%**), indicating that device type is not the primary driver of funnel loss.
* **Behavioral Correlations:**
  * `add_to_cart_flag` vs. `purchase_flag`: **$r = 0.7285$** (strong positive sequential relationship)
  * `page_views` vs. `time_on_site_sec`: **$r = 0.8041$** (strong engagement depth correlation)
  * `page_views` vs. `purchase_flag`: **$r = -0.0006$** (negligible linear correlation)
  * `time_on_site_sec` vs. `purchase_flag`: **$r = 0.0042$** (negligible linear correlation)

---

## Conversion Funnel Summary

| Funnel Step | User Sessions | Overall Conversion | Step-to-Step Retention | Step-to-Step Drop-off |
| :--- | :---: | :---: | :---: | :---: |
| **1. Session Start** | 5,000 | 100.00% | 100.00% | — |
| **2. Add to Cart** | 1,470 | 29.40% | 29.40% | 70.60% |
| **3. Purchase** | 905 | 18.10% | 61.56% | 38.44% |

---

## Dataset & Data Hygiene

The synthetic dataset (`ga4_sample_session_logs.csv`) was generated using `seed = 42` for full reproducibility and contains **5,000 rows × 8 columns**:

| Column | Type | Description |
| :--- | :--- | :--- |
| `session_id` | `string` | Unique session identifier |
| `user_id` | `string` | Synthetic user identifier (allows repeat sessions) |
| `device_category` | `string` | Standardized device type (`desktop`, `mobile`, `tablet`) |
| `session_start_flag` | `int` | Binary indicator (`1` = session initiated) |
| `add_to_cart_flag` | `int` | Binary indicator (`1` = item added to cart) |
| `purchase_flag` | `int` | Binary indicator (`1` = purchase completed) |
| `page_views` | `int` | Total pages viewed during the session |
| `time_on_site_sec` | `float` | Session duration in seconds |

**Cleaning Pipeline:**
1. **Missing Value Imputation:** Detected 50 missing entries in `time_on_site_sec` and imputed them using the pre-imputation median (**144 seconds**), resulting in zero missing cells.
2. **Category Standardization:** Applied lowercase and whitespace stripping to `device_category` to ensure consistent grouping.

---

