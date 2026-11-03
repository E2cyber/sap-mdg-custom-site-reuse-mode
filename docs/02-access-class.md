# Phase 2: Access Class Implementation

## Overview

The Access Class is the core component that handles all data operations between MDG and the custom ERP table `YMDG_SITE`. It implements the interface `IF_USMD_PP_ACCESS` which provides methods for reading, writing, locking, and querying data.

**Class Name:** `ZCL_MDG_SITE_ACCESS`

---

## 2.1 Create Access Class

### Step 1: Create Class

1. Open transaction **SE24**
2. Enter class name: `ZCL_MDG_SITE_ACCESS`
3. Click **Create**

![Class Creation](images/phase2/class-creation.png)

---

### Step 2: Provide Class Details

![Class Description and Instantiation](images/phase2/class-description.png)

**Configuration:**
- **Description:** MDG Site Access Class
- **Instantiation:** Public
- **Class Type:** Usual ABAP Class

4. Click **Save** (assign to package or local object)

---

### Step 3: Add Interface

1. Navigate to **Interfaces** tab
2. Click **Add Interface** button
3. Enter interface name: `IF_USMD_PP_ACCESS`

![Interface Assignment](images/phase2/interface-assignment.png)

4. Press **Enter** to confirm

---

### Step 4: Review Methods

1. Navigate to **Methods** tab
2. You should see all interface methods listed:

![Methods Tab](images/phase2/methods-tab.png)

**Methods to Implement:**
- `CHECK_EXISTENCE_MASS` - Check if records exist in active area
- `DEQUEUE` - Unlock records
- `ENQUEUE` - Lock records
- `GET_KEY_HANDLING` - Define key handling strategy
- `GET_QUERY_PROPERTIES` - Define searchable fields
- `QUERY` - Search functionality
- `READ_VALUE` - Read data from active area
- `SAVE` - Persist data to YMDG_SITE table

**Note:** Based on your business requirement, you can implement the necessary methods. For this implementation, we'll implement all core methods.

---

## 2.2 Implement Methods

### Method 1: CHECK_EXISTENCE_MASS

**Purpose:** Check if Site IDs already exist in the YMDG_SITE table

Click on method `IF_USMD_PP_ACCESS~CHECK_EXISTENCE_MASS` and add this code:

```abap
METHOD if_usmd_pp_access~check_existence_mass.

  TYPES: BEGIN OF ty_key,
           zsite_id TYPE zsite_id,
         END OF ty_key.

  DATA: lt_key_check TYPE STANDARD TABLE OF ty_key,
        lt_key_db    TYPE STANDARD TABLE OF ty_key,
        ls_key       TYPE ty_key.

  FIELD-SYMBOLS: <ls_input_key> TYPE any,
                 <lv_site_id>   TYPE any.

  CLEAR: et_key,
         et_message,
         ev_not_supported.

  ev_not_supported = abap_false.

  " Only handle SITE entity
  IF iv_entity <> 'SITE'.
    ev_not_supported = abap_true.
    RETURN.
  ENDIF.

  IF it_key IS INITIAL.
    RETURN.
  ENDIF.

  " Extract Site IDs from input
  LOOP AT it_key ASSIGNING <ls_input_key>.
    ASSIGN COMPONENT 'ZSITE_ID' OF STRUCTURE <ls_input_key> TO <lv_site_id>.
    IF sy-subrc = 0.
      ls_key-zsite_id = <lv_site_id>.
      APPEND ls_key TO lt_key_check.
    ENDIF.
  ENDLOOP.

  " Check existence in YMDG_SITE table
  IF lt_key_check IS NOT INITIAL.
    SELECT zsite_id
      FROM ymdg_site
      INTO TABLE lt_key_db
      FOR ALL ENTRIES IN lt_key_check
      WHERE zsite_id = lt_key_check-zsite_id.
  ENDIF.

  " Return existing keys
  LOOP AT it_key ASSIGNING <ls_input_key>.
    ASSIGN COMPONENT 'ZSITE_ID' OF STRUCTURE <ls_input_key> TO <lv_site_id>.
    IF sy-subrc = 0.
      ls_key-zsite_id = <lv_site_id>.
      READ TABLE lt_key_db TRANSPORTING NO FIELDS
        WITH KEY zsite_id = ls_key-zsite_id.
      IF sy-subrc = 0.
        INSERT <ls_input_key> INTO TABLE et_key.
      ENDIF.
    ENDIF.
  ENDLOOP.

ENDMETHOD.
