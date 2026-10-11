# Contract - Supplier Sourcing and Rating Platform for General Contractors

> **Course Project:** Software Engineering for Civil Technology (Assignment #2)  
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

## 2. Website Architecture & Implementation Priorities (Mermaid Diagram)

The following Mermaid graph outlines the site layout and implementation priorities for MVP development.

```mermaid
graph TD
    %% Priority Styling Definitions
    classDef high fill:#ff9999,stroke:#333,stroke-width:2px,color:#000;
    classDef medium fill:#ffcc99,stroke:#333,stroke-width:1.5px,color:#000;
    classDef low fill:#ffff99,stroke:#333,stroke-width:1px,color:#000;

    %% Root Node
    Home["Contract Platform Landing Page"]

    %% Main Modules
    SupplierModule["1. Supplier Directory Module"]
    SourcingModule["2. Project Sourcing & Comparison"]
    RatingModule["3. Performance Rating & Scorecards"]
    AdminModule["4. Project & System Admin"]

    %% Sub-pages & Features
    SupReg["Supplier Pre-Qualification & Reg"]
    CatMgmt["Material Catalog & Pricing/Delivery"]
    
    ReqDefine["Project Material Requirements"]
    CostCompare["Landed Cost Real-time Comparison"]
    PlaceOrder["Purchase Order Issuance"]

    PostRating["Post-Delivery Rating Mechanism"]
    VendorScorecard["Vendor Scorecards & Reports"]
    Blacklist["Supplier Blacklist / Flagging"]

    ProjMgmt["Project Creation & Permissions"]
    ScheduleSync["Schedule Sync & Auto-Adjustment"]

    %% Architecture Links
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

    %% Priority Class Assignment
    class Home,SupplierModule,SourcingModule,SupReg,CatMgmt,ReqDefine,CostCompare high;
    class RatingModule,AdminModule,PlaceOrder,PostRating,ProjMgmt medium;
    class VendorScorecard,Blacklist,ScheduleSync low;
