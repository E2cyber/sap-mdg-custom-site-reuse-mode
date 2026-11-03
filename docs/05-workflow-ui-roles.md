# Phase 5-7: Workflow, UI & Role Model

## Overview

Phases 5, 6, and 7 cover the MDG frontend configuration including workflow, user interface, and security roles. **These configurations are identical for both Flex Mode and Reuse Mode implementations.**

Since the custom SITE entity is now properly configured with the data model, access class, and mappings, the remaining configuration follows standard MDG processes.

---

## Reference Implementation Guide

For detailed step-by-step instructions for Phases 5-7, follow the SAP Community implementation guide:

📚 **[How to Develop a Custom Object with MDG Central Governance](https://www.sap.com/documents/2019/08/94691341-5d7d-0010-87a3-c30de2ffd8ff.html)**

**Note:** The workflow, UI, and role model configurations described in the guide apply equally to both Flex Mode and Reuse Mode implementations. No additional adjustments are needed for Reuse Mode.

---

## ✅ Combined Checklist (Phases 5-7)

### Phase 5: Workflow & Process Modeling
- [ ] Change Request Type created
- [ ] Process Model configured
- [ ] Workflow steps defined
- [ ] Approval routing configured
- [ ] Business Activity assigned to SITE entity

### Phase 6: User Interface
- [ ] Search fields configured
- [ ] Object page layout defined
- [ ] All 7 fields displayed (SITE, NAME, CITY, COUNTRY, STREET, ZIP, DESCR)
- [ ] Field properties set (mandatory, optional, read-only)
- [ ] UI tested in NWBC

### Phase 7: Role Model
- [ ] Requester role created
- [ ] Approver role created
- [ ] Administrator role created
- [ ] Authorization objects configured
- [ ] Test users assigned to roles

---

## 💡 Key Points

- **No Reuse Mode Differences:** Phases 5-7 are configured identically regardless of Flex or Reuse Mode
- **Standard MDG Config:** Use standard SAP MDG configuration guide
- **Test Incrementally:** Test each phase before moving to the next
- **User Training:** Document the configured workflows for end users

---

## 🔜 Next Step

Proceed to [Phase 8: Testing](06-testing.md)

Once Phases 5-7 are completed, you'll be ready to perform end-to-end testing of the entire solution.

---

## ⚠️ Important Notes

1. **Follow the Reference Guide:** The SAP Community guide provides detailed screenshots and step-by-step instructions
2. **No Custom Code Needed:** All configuration is done through MDGIMG and PFCG
3. **Test Each Phase:** Complete testing before moving to the next phase
4. **Document Changes:** Keep track of all configuration for future reference
5. **Transport Management:** Ensure all config is captured in transport requests

---
