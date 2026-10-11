# Contract - Supplier Sourcing and Rating Platform for General Contractors

> **Course Project:** Software Engineering for Civil Technology (Assignment #2)  
> **Team Members:** Dimas Dermawan (M11402826) | 陳韋翰 (M11505112)  
> **Repository:** https://github.com/den-dimas/contract

---

## 1. Project Background & Value Proposition

Material purchases represent **40–60%** of a construction project's total budget, yet contractors face tight **2–5%** profit margins. Price errors and missed rebates cause **4–8%** of material budgets to leak out due to manual processes via spreadsheets and phone calls. 

**Contract** is a supplier sourcing and performance rating platform specifically designed for mid-market General Contractors (GCs). It turns every completed delivery into actionable performance data to optimize procurement decisions over time.

### Core MVP Features
* **Supplier Directory:** Register vendors, qualification certificates, and material catalogs.
* **Project Sourcing Engine:** Compare real landed cost (Material Price + Delivery Rate per km) side by side.
* **Performance Rating System:** Post-delivery scoring on on-time delivery and quantity accuracy fed into future supplier rankings.

---

## 2. Website Architecture & Team Assignment (Mermaid Diagram)

The following Mermaid graph outlines the site layout, team responsibilities, and implementation priorities for MVP development.

```mermaid
graph TD
    Home["Landing Page (Lead: Dimas)"]

    SupplierModule["1. Supplier Directory Module (Lead: 陳韋翰)"]
    SourcingModule["2. Project Sourcing and Comparison (Lead: Dimas)"]
    RatingModule["3. Performance Rating and Scorecards (Lead: 陳韋翰)"]
    AdminModule["4. Project and System Admin (Lead: Dimas)"]

    SupReg["Supplier Pre-Qualification (Lead: 陳韋翰)"]
    CatMgmt["Material Catalog and Pricing (Lead: 陳韋翰)"]
    
    ReqDefine["Project Material Requirements (Lead: Dimas)"]
    CostCompare["Landed Cost Comparison Engine (Lead: Dimas)"]
    PlaceOrder["Purchase Order Issuance (Lead: Dimas)"]

    PostRating["Post-Delivery Rating Mechanism (Lead: 陳韋翰)"]
    VendorScorecard["Vendor Scorecards and Reports (Lead: 陳韋翰)"]
    Blacklist["Supplier Blacklist and Flagging (Lead: 陳韋翰)"]

    ProjMgmt["Project Creation and Permissions (Lead: Dimas)"]
    ScheduleSync["Schedule Sync and Auto-Adjustment (Lead: Dimas)"]

    Home --> SupplierModule
    Home --> SourcingModule
    Home --> RatingModule
    Home --> AdminModule

    SupplierModule --> SupReg
    SupplierModule --> CatMgmt

    SourcingModule --> ReqDefine
    SourcingModule --> CostCompare
    SourcingModule --> PlaceOrder

    RatingModule --> PostRating
    RatingModule --> VendorScorecard
    RatingModule --> Blacklist

    AdminModule --> ProjMgmt
    AdminModule --> ScheduleSync
    ```markdown
---

## 6. Detailed User Stories

* **As a GC Project Manager (PM):**
  * I want to specify required material quantities for a project so that I can automatically calculate and compare the total landed cost across all matching suppliers.
  * I want to rate suppliers on delivery accuracy and punctuality after each fulfillment so that my team can maintain a reliable track record for future procurement.
* **As a GC Executive / Admin:**
  * I want to add new team members to our company account with per-seat billing updates so that our expanding procurement team can collaborate securely.
  * I want to review system audit logs to track who modified specific purchase orders or supplier ratings for full transparency.
* **As a Material Supplier:**
  * I want to list my raw material catalog, unit prices, and per-kilometer delivery rates so that I can receive qualified quote requests from contractors.

---

## 7. Technical Architecture & System Specs

### Tech Stack Selection (MVP)
* **Frontend:** Next.js (React), Tailwind CSS, Mermaid.js
* **Backend:** Node.js (Express) / Python FastAPI
* **Database:** PostgreSQL (Relational schema with multi-tenant isolation and audit tables)
* **Authentication & Billing:** NextAuth.js / Auth0 + Stripe API (Seat subscription management)

### Landed Cost Calculation Logic
$$\text{Total Landed Cost} = (\text{Unit Material Price} \times \text{Quantity}) + (\text{Distance in km} \times \text{Delivery Rate per km}) + \text{Tax}$$

---

## 8. Database Schema Design (Key Tables)

| Table Name | Primary Fields | Description |
| :--- | :--- | :--- |
| **`organizations`** | `id`, `company_name`, `tenant_id`, `plan_tier`, `max_seats`, `active_seats` | Master enterprise tenant data and seat license limits. |
| **`users`** | `id`, `org_id`, `email`, `role`, `name`, `seat_status` | Individual user accounts mapped to corporate roles and seats. |
| **`audit_logs`** | `id`, `org_id`, `user_id`, `action_type`, `entity_type`, `entity_id`, `changes_json`, `timestamp`, `ip_address` | System-wide audit log recording every user modification. |
| **`suppliers`** | `id`, `company_name`, `license_no`, `rating_score` | Vendor directory and pre-qualification status. |
| **`materials`** | `id`, `supplier_id`, `material_type`, `unit_price`, `delivery_rate_km` | Product catalogs, pricing, and freight rates per km. |
| **`orders`** | `id`, `project_id`, `supplier_id`, `version_id`, `total_landed_cost`, `updated_by_user_id` | Purchase orders with optimistic concurrency locking. |
| **`ratings`** | `id`, `order_id`, `created_by_user_id`, `punctuality_score`, `quantity_score` | Post-delivery ratings tied to specific field inspectors. |

---

## 9. Core RESTful API Endpoints

* `GET /api/v1/suppliers` - Fetch filtered supplier directory by location and material.
* `POST /api/v1/sourcing/compare` - Submit project requirements and calculate landed costs.
* `POST /api/v1/orders` - Issue a new purchase order to a selected supplier.
* `POST /api/v1/ratings` - Submit a post-delivery performance rating.
* `POST /api/v1/org/seats/invite` - Invite a new user seat (triggers per-seat billing charge).
* `GET /api/v1/admin/audit-logs` - Query historical modification logs filtered by user, timestamp, or entity.

---

## 10. Feasibility Enhancements & Solutions

To strengthen platform adoption and data trustworthiness, we propose four feasible enhancement solutions:

1. **Single-Sided Tooling (Excel/CSV Import):**
   * *Problem:* Cold-start issues when suppliers have not yet registered.
   * *Solution:* Allow GCs to import their existing supplier spreadsheets so the platform functions immediately as a private vendor directory without waiting for supplier onboarding.
2. **Proof-of-Delivery (PoD) Photo Verification:**
   * *Problem:* Subjective rating bias from field workers.
   * *Solution:* Enable field staff to upload delivery receipt photos, automatically validating delivered vs. ordered quantities to back ratings with verifiable proof.
3. **Interactive ROI Calculator:**
   * *Problem:* Demonstrating value for the flat monthly fee ($199 Starter / $499 Growth).
   * *Solution:* Integrate an ROI calculator showing how preventing a 1% pricing error on a single concrete order yields $2,000+ in savings.
4. **Multi-Tenancy Data Isolation:**
   * *Problem:* GC concerns over leaking confidential pricing to competitors.
   * *Solution:* Enforce strict tenant-level data isolation, ensuring custom supplier ratings and historical quotes remain strictly private to GC executives.
