# Phase 1: DDIC Objects (Custom Tables & Structures)

## Overview

The first step is to create the Data Dictionary (DDIC) objects required for the custom Site master data object. These objects define how the data is stored, processed, and locked within the system. 

**In this implementation, the approved Site records will be stored directly in the custom ERP table `YMDG_SITE`.**

---

## 1.1 Create Domain and Data Element for SITE_ID

### Step 1: Create Domain ZDOM_SITE_ID

1. Open transaction **SE11**
2. Select **Domain**
3. Enter name: `ZDOM_SITE_ID`
4. Click **Create**
5. Configure:
   - **Data Type:** CHAR
   - **Length:** 10
   - **Output Length:** 10
6. **Save** (assign to package or local object)
7. **Activate**

![Domain Creation](images/phase1/domain-creation.png)

---

### Step 2: Create Data Element ZSITE_ID

1. Open transaction **SE11**
2. Select **Data Type** → **Data Element**
3. Enter name: `ZSITE_ID`
4. Click **Create**
5. Configure:
   - **Domain:** ZDOM_SITE_ID
   - **Field Label:**
     - Short: Site ID
     - Medium: Site ID
     - Long: Site ID
     - Heading: Site ID
6. **Save** and **Activate**

---

## 1.2 Create Main ERP Table YMDG_SITE

### Transaction: SE11

1. Select **Database Table**
2. Enter name: `YMDG_SITE`
3. Click **Create**

### Configuration:

**Delivery and Maintenance Tab:**
- **Delivery Class:** A (Application table)
- **Data Browser/Table View Maintenance:** Display/Maintenance Allowed with Restrictions

### Fields Definition:

| Field Name | Key | Data Element | Description |
|------------|-----|--------------|-------------|
| MANDT | ✓ | MANDT | Client |
| ZSITE_ID | ✓ | ZSITE_ID | Site ID |
| AD_NAME1 | | AD_NAME1 | Name |
| AD_CITY1 | | AD_CITY1 | City |
| LAND1 | | LAND1 | Country |
| AD_STREET | | AD_STREET | Street |
| AD_PSTCD1 | | AD_PSTCD1 | Postal Code |
| AD_REMARK1 | | AD_SMTPADR | Description |

### Enhancement Category:

1. Go to **Extras** → **Enhancement Category**
2. Select: **Can be Enhanced (Deep)**

### Technical Settings:

1. Press **Ctrl+Shift+F9** (or click Technical Settings button)
2. Configure:
   - **Data Class:** APPL0 (Master data)
   - **Size Category:** 1 (or as per requirement)
3. **Save** and **Activate**

---

## 1.3 Create Supporting Structures

### A. Structure ZMDG_SITE_S

**Purpose:** Main data structure for Site entity

1. Transaction: **SE11**
2. Select **Data Type** → **Structure**
3. Name: `ZMDG_SITE_S`
4. Click **Create**

**Fields:**

| Field Name | Component Type | Description |
|------------|----------------|-------------|
| ZSITE_ID | ZSITE_ID | Site ID |
| AD_NAME1 | AD_NAME1 | Name |
| AD_CITY1 | AD_CITY1 | City |
| LAND1 | LAND1 | Country |
| AD_STREET | AD_STREET | Street |
| AD_PSTCD1 | AD_PSTCD1 | Postal Code |
| AD_REMARK1 | AD_REMARK1 | Description |

5. **Extras** → **Enhancement Category** → **Can be Enhanced (Deep)**
6. **Save** and **Activate**

---

### B. Structure ZMDG_SITE_S_X

**Purpose:** Change indicator structure (X-structure)

1. Transaction: **SE11**
2. Name: `ZMDG_SITE_S_X`
3. Click **Create**

**Fields:**

|Component|Typing Method|Component Type|
|------------|----------------|-------------|
| ZSITE ID | Types | ZSITE ID |
| AD NAME1 | Types | AD NAME1 |
| AD CITY1 | Types | AD CITY1 |
| LAND1 | Types | LAND1 |
| AD STREET | Types | AD STREET |
| AD PSTCD1 | Types | AD PSTCD1 |
| AD REMARK1 |	Types | AD REMARK1 |
| XFELD | Types | XFELD |



4. **Enhancement Category:** Can be Enhanced (Deep)
5. **Save** and **Activate**

---

## 1.4 Create Table Types

### A. Table Type ZMDG_SITE_T

**Purpose:** Table type for Site data

1. Transaction: **SE11**
2. Select **Data Type** → **Table Type**
3. Name: `ZMDG_SITE_T`
4. Click **Create**

**Configuration:**
- **Line Type:** ZMDG_SITE_S
- **Access:** Sorted Table
- **Key Category:** Unique
- **Key Component:** ZSITE_ID

5. **Save** and **Activate**

---

### B. Table Type ZMDG_SITE_T_X

**Purpose:** Table type for change indicators

1. Transaction: **SE11**
2. Name: `ZMDG_SITE_T_X`
3. Click **Create**

**Configuration:**
- **Line Type:** ZMDG_SITE_S_X
- **Access:** Sorted Table
- **Key Category:** Unique
- **Key Component:** ZSITE_ID

4. **Save** and **Activate**

---

## 1.5 Create Lock Object EZMDG_SITE

**Purpose:** Ensure data consistency during concurrent access

1. Transaction: **SE11**
2. Select **Lock Object**
3. Name: `EZMDG_SITE`
4. Click **Create**

**Configuration:**
- **Primary Table Name:** YMDG_SITE
- **Lock Mode:** Write Lock (E - Exclusive)

**Lock Parameters:**

| Parameter Name | Type |
|----------------|------|
| MANDT | Client |
| ZSITE_ID | Site ID |

5. **Save** and **Activate**

**Note:** This generates two function modules automatically:
- `ENQUEUE_EZMDG_SITE` (for locking)
- `DEQUEUE_EZMDG_SITE` (for unlocking)

---

## ✅ Phase 1 Checklist

Before proceeding to Phase 2, ensure:

- [ ] Domain ZDOM_SITE_ID created and activated
- [ ] Data Element ZSITE_ID created and activated
- [ ] Table YMDG_SITE created and activated
- [ ] Structure ZMDG_SITE_S created and activated
- [ ] Structure ZMDG_SITE_S_X created and activated
- [ ] Table Type ZMDG_SITE_T created and activated
- [ ] Table Type ZMDG_SITE_T_X created and activated
- [ ] Lock Object EZMDG_SITE created and activated

---

## 📊 Objects Summary

| Object Type | Object Name | Purpose |
|-------------|-------------|---------|
| Domain | ZDOM_SITE_ID | Site ID domain |
| Data Element | ZSITE_ID | Site ID data element |
| Table | YMDG_SITE | Active area storage |
| Structure | ZMDG_SITE_S | Main data structure |
| Structure | ZMDG_SITE_S_X | Change indicator structure |
| Table Type | ZMDG_SITE_T | Table type for data |
| Table Type | ZMDG_SITE_T_X | Table type for changes |
| Lock Object | EZMDG_SITE | Locking mechanism |

---

## 🔜 Next Step

Proceed to [Phase 2: Access Class Implementation](02-access-class.md)

---

## 💡 Tips

- Use consistent naming conventions (Z prefix for custom objects)
- Always assign enhancement category for future extensibility
- Document your objects in transport requests
- Test lock object by checking generated function modules (SE37)
