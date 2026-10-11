# Contract - Supplier Sourcing and Rating Platform for General Contractors

> **Course Project:** Software Engineering for Civil Technology (Assignment #2)  
> **Team Members:** Dimas Dermawan (M11402826) | 陳韋翰 (M11505112)  
> **Repository:** https://github.com/den-dimas/contract

---

## 1. Project Background & Value Proposition

Material purchases represent **40–60%** of a construction project's total budget, yet contractors face tight **2–5%** profit margins. Price errors and missed rebates cause **4–8%** of material budgets to leak out. 

**Contract** is a supplier sourcing and performance rating platform specifically designed for mid-market General Contractors (GCs). It turns every completed delivery into actionable performance data to optimize procurement decisions over time.

### Core MVP Features
* **Supplier Directory:** Register vendors, qualification certificates, and material catalogs.
* **Project Sourcing:** Compare real landed cost (Material Price + Delivery Rate) side by side.
* **Performance Rating:** Post-delivery scoring on on-time delivery and quantity accuracy.

---

## 2. Website Architecture & Team Assignment (Mermaid Diagram)

The following Mermaid graph outlines the site layout, team responsibilities, and implementation priorities for MVP development.

```mermaid
graph TD
    %% Priority Styling Definitions
    classDef high fill:#ff9999,stroke:#333,stroke-width:2px,color:#000;      %% 🔴 High Priority (MVP Core)
    classDef medium fill:#ffcc99,stroke:#333,stroke-width:1.5px,color:#000;  %% 🟠 Medium Priority
    classDef low fill:#ffff99,stroke:#333,stroke-width:1px,color:#000;       %% 🟡 Low Priority (Future Phase)

    %% Root
    Home[Contract Platform Landing Page <br> Lead: Dimas]

    %% Main Modules
    SupplierModule[1. Supplier Directory Module <br> Lead: 陳韋翰]
    SourcingModule[2. Project Sourcing & Comparison <br> Lead: Dimas]
    RatingModule[3. Performance Rating & Scorecards <br> Lead: 陳韋翰]
    AdminModule[4. Project & System Admin <br> Lead: Dimas]

    %% Sub-pages & Features
    SupReg[Supplier Pre-Qualification & Reg <br> Lead: 陳韋翰]
    CatMgmt[Material Catalog & Pricing/Delivery <br> Lead: 陳韋翰]
    
    ReqDefine[Project Material Requirements <br> Lead: Dimas]
    CostCompare[Landed Cost Real-time Comparison <br> Lead: Dimas]
    PlaceOrder[Purchase Order Issuance <br> Lead: Dimas]

    PostRating[Post-Delivery Rating Mechanism <br> Lead: 陳韋翰]
    VendorScorecard[Vendor Scorecards & Reports <br> Lead: 陳韋翰]
    Blacklist[Supplier Blacklist / Flagging <br> Lead: 陳韋翰]

    ProjMgmt[Project Creation & Permissions <br> Lead: Dimas]
    ScheduleSync[Schedule Sync & Auto-Adjustment <br> Lead: Dimas]

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
