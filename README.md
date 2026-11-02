# How to Create a Custom Object with Reuse Mode in SAP MDG

![SAP](https://img.shields.io/badge/SAP-MDG-0FAAFF?style=flat-square&logo=sap)
![ABAP](https://img.shields.io/badge/ABAP-OO-00599C?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

> **A step-by-step guide to implementing custom master data governance using SAP MDG Reuse Mode with direct persistence to custom ERP tables.**

---

## 📖 Introduction

In many SAP MDG implementations, there is a need to govern custom master data objects that do not fit into the standard data models provided by SAP. In our case, the requirement was to manage **Site master data** through an approval process and store the approved records directly in a custom ERP table, **YMDG_SITE**.

To achieve this, we implemented a custom object using **SAP MDG Reuse Mode**. Users can create and maintain site records through MDG, submit them for approval, and once approved, the data is automatically persisted in the custom ERP table.

### 🎯 Why This Approach?

This approach allows organizations to:
- ✅ Leverage MDG's governance capabilities (change requests, workflows, validations, approvals)
- ✅ Keep master data in their own custom ERP tables
- ✅ Maintain full control over data structures
- ✅ Integrate custom objects with standard MDG processes

---

## 💼 Business Scenario

**Challenge:** Need to manage custom Site master data that doesn't exist in standard SAP models.

**Solution:** Implement custom Site object in MDG with:
- Approval workflow for all changes
- Validation rules
- Direct storage in custom table YMDG_SITE
- Search and maintenance capabilities

**Outcome:** Governed master data management for custom objects with full MDG capabilities.

---

## 🏗️ Solution Architecture

| Component | Description |
|-----------|-------------|
| **MDG Mode** | Reuse Mode (direct persistence to custom tables) |
| **Data Model** | ZK (Custom) |
| **Entity** | SITE |
| **Active Table** | YMDG_SITE (Custom ERP table) |
| **Access Class** | ZCL_MDG_SITE_ACCESS |
| **Interface** | IF_USMD_PP_ACCESS |

---

## 📋 Implementation Guide

Follow these phases to implement your own custom object:

### Phase 1: [DDIC Objects (Custom Tables & Structures)](docs/01-ddic-objects.md)
Create the foundation:
- Domain & Data Element for Site ID
- Main ERP Table (YMDG_SITE)
- Supporting Structures (ZMDG_SITE_S, ZMDG_SITE_S_X)
- Table Types (ZMDG_SITE_T, ZMDG_SITE_T_X)
- Lock Object (EZMDG_SITE)

### Phase 2: [Access Class Implementation](docs/02-access-class.md)
Implement the data access layer:
- Create class `ZCL_MDG_SITE_ACCESS`
- Implement interface `IF_USMD_PP_ACCESS`
- Methods: READ_VALUE, QUERY, SAVE, ENQUEUE, DEQUEUE, CHECK_EXISTENCE_MASS

### Phase 3: [Data Model Setup with Reuse Area](docs/03-data-model-setup.md)
Configure MDG framework:
- Create Data Model ZK
- Define Entity Type SITE
- Configure Reuse Active Area (ZK_SITE_AR)
- Link Access Class

### Phase 4: [SMT Mappings](docs/04-smt-mappings.md)
Set up data transformation:
- Active Area → Staging Area mapping (Z_MAP_SITE_2_STA)
- Staging Area → Active Area mapping (Z_MAP_SITE_2_PP)
- Field-level mappings

### Phase 5-7: [Workflow, UI & Role Model](docs/05-workflow-ui-roles.md)
Complete the solution:
- Process Modeling & Workflow
- User Interface Configuration
- Role Model Setup

### Phase 8: [Testing](docs/06-testing.md)
Validate the implementation:
- Create Site records
- Submit for approval
- Verify data persistence in YMDG_SITE table

---

## 📂 What's Inside

```text
.
├── config/
│   └── Configuration documentation
├── docs/
│   └── Detailed implementation guides
├── src/
│   ├── classes/
│   │   └── ABAP access class code
│   └── ddic/
│       └── Data dictionary objects
├── LICENSE
└── README.md
```

---

## 🎓 What You'll Learn

By following this guide, you'll understand:
- How to implement custom objects in SAP MDG
- Difference between Reuse Mode and Flex Mode
- Access class development for custom persistence
- Data model configuration in MDG
- SMT mapping setup
- End-to-end MDG implementation process

---

## 🛠️ Prerequisites

**System Requirements:**
- SAP S/4HANA or ECC with MDG component installed
- ABAP development authorization
- MDG configuration authorization (transaction MDGIMG)

**Knowledge Requirements:**
- Basic understanding of SAP MDG concepts
- ABAP programming
- Data modeling fundamentals

---

## 📸 Screenshots & Visuals

All implementation steps include screenshots showing:
- DDIC object creation in SE11
- Access class code in SE24
- Data model configuration in MDGIMG
- SMT mapping setup
- UI testing in NWBC
- Final data verification in SE16N

---

## 💡 When to Use This Pattern

This implementation pattern is ideal when:
- You need to govern custom master data not covered by standard MDG models
- Your organization has proprietary data objects requiring approval workflows
- You want direct control over data persistence (custom tables)
- You need to extend MDG capabilities to custom scenarios
- You want to integrate custom data with standard MDG processes

---

## 🔄 Reuse Mode vs Flex Mode

**Reuse Mode (This Guide):**
- ✅ Data stored in custom active area tables (e.g., YMDG_SITE)
- ✅ Direct persistence to your own tables
- ✅ Full control over data structure
- ✅ Requires custom access class

**Flex Mode:**
- Data stored in MDG generic tables
- Faster implementation
- Less flexibility in data structure

---

## 👤 Author

**Naveen Neelakandan**  
SAP MDG Consultant  

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🤝 How to Use This Repository

1. **Read the overview** (this README)
2. **Follow the phases** in sequence (docs folder)
3. **Adapt the code** to your custom object
4. **Test thoroughly** in development system
5. **Share your feedback** via issues or pull requests

---

## 📚 Additional Resources

- [SAP MDG Official Documentation](https://help.sap.com/docs/SAP_MASTER_DATA_GOVERNANCE)
- [SAP Community - MDG Topics](https://community.sap.com/t5/technology-blog-posts-by-members/how-to-create-a-custom-object-with-reuse-mode-in-sap-mdg/ba-p/14456559)

---

## ⭐ Found This Helpful?

If this guide helped you implement custom objects in SAP MDG, please:
- ⭐ **Star this repository**
- 🔄 **Share with your network**
- 💬 **Leave feedback or questions in Issues**

---

## 📞 Questions or Issues?

Open an issue in this repository, and I'll be happy to help!

---

**Happy Implementing! 🚀**
