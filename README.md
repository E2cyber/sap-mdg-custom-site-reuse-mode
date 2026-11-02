# SAP MDG Custom Object – Site Master (Reuse Mode)

![SAP](https://img.shields.io/badge/SAP-MDG-0FAAFF?style=flat-square&logo=sap)
![ABAP](https://img.shields.io/badge/ABAP-00599C?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

## 📋 Overview

Implementation of custom **Site Master Data** governance using **SAP MDG Reuse Mode**. This solution enables organizations to manage site records through MDG's approval workflow while persisting approved data directly to a custom ERP table `YMDG_SITE`.

### Key Features
- ✅ Custom master data governance using MDG Reuse Mode
- ✅ Change request management with approval workflow
- ✅ Direct persistence to custom ERP table (YMDG_SITE)
- ✅ Full CRUD operations (Create, Read, Update, Delete)
- ✅ Lock management and data validation
- ✅ Search and query capabilities

---

## 🏗️ Architecture

| Component | Value |
|-----------|-------|
| **MDG Mode** | Reuse Mode |
| **Data Model** | ZK |
| **Entity** | SITE |
| **Active Table** | YMDG_SITE |
| **Access Class** | ZCL_MDG_SITE_ACCESS |
| **Interface** | IF_USMD_PP_ACCESS |

---

## 🚀 Implementation Phases

### Phase 1: [DDIC Objects](docs/01-ddic-objects.md)
- Domain & Data Element (ZSITE_ID)
- Main ERP Table (YMDG_SITE)
- Structures (ZMDG_SITE_S, ZMDG_SITE_S_X)
- Table Types (ZMDG_SITE_T, ZMDG_SITE_T_X)
- Lock Object (EZMDG_SITE)

### Phase 2: [Access Class Implementation](docs/02-access-class.md)
- `ZCL_MDG_SITE_ACCESS` implementing `IF_USMD_PP_ACCESS`
- Methods: ENQUEUE, DEQUEUE, READ_VALUE, QUERY, SAVE, CHECK_EXISTENCE_MASS

### Phase 3: [Data Model Setup](docs/03-data-model-setup.md)
- Data Model ZK configuration
- Reuse Active Area: ZK_SITE_AR
- Entity Type: SITE

### Phase 4: [SMT Mappings](docs/04-smt-mappings.md)
- Active Area → Staging Area (Z_MAP_SITE_2_STA)
- Staging Area → Active Area (Z_MAP_SITE_2_PP)

### Phase 5-7: [Workflow, UI & Roles](docs/05-workflow-ui-roles.md)
- Process Modeling
- User Interface Configuration
- Role Model Setup

### Phase 8: [Testing](docs/06-testing.md)
- End-to-end testing scenarios
- Data persistence verification

---

## 📂 Repository Structure

├── config/                 # Configuration documentation
├── docs/                   # Detailed implementation guides
├── src/
│   ├── classes/            # ABAP access class code
│   └── ddic/               # Data dictionary objects
├── LICENSE
└── README.md

---

## 🛠️ Prerequisites

- SAP S/4HANA or ECC with MDG component
- ABAP development authorization
- MDG configuration authorization
- Basic knowledge of:
  - SAP MDG architecture
  - ABAP programming
  - Data modeling concepts

---

## 📸 Screenshots

Implementation screenshots are available in the `docs/images/` folder showing:
- DDIC object creation
- Access class implementation
- Data model configuration
- SMT mapping setup
- UI testing results

---

## 💡 Use Cases

This implementation pattern is suitable for:
- Custom master data not covered by standard MDG models
- Organizations requiring governance for proprietary data objects
- Scenarios requiring direct ERP table persistence
- Custom extensions to standard MDG functionality

---

## 👤 Author

**Naveen Neelakandan**  
SAP MDG Consultant

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing

Feel free to fork this project and adapt it to your requirements. If you have suggestions for improvements, please open an issue.

---

## 📚 References

- [SAP MDG Documentation](https://help.sap.com/docs/SAP_MASTER_DATA_GOVERNANCE)
- [How to Develop Custom Object with MDG Central Governance](https://community.sap.com/t5/technology-blog-posts-by-members/how-to-create-a-custom-object-with-reuse-mode-in-sap-mdg/ba-p/14456559)

---

**⭐ If you find this helpful, please star this repository!**

