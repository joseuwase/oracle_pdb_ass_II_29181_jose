# Oracle Pluggable Database Assignment II

**Student Name:** Jose  
**Student ID:** 29181  
**Course:** Database Development with PL/SQL (INSY 8311)  
**Instructor:** Eric Maniraguha  
**Date:** February 15, 2026

---

## Overview

This assignment demonstrates practical skills in Oracle Multitenant Architecture, focusing on:
- Creating and managing Pluggable Databases (PDBs)
- User creation and management within PDBs
- Using Oracle Enterprise Manager (OEM)
- Professional technical documentation

---

## Oracle Environment

- **Oracle Version:** 21c Express Edition
- **Platform:** Microsoft Windows x86 64-bit
- **Container Database (CDB):** XE
- **Number of PDBs Created:** 3 (jo_pdb_29181, jo_to_delete_pdb_29181, XEPDB1)

---

## Task 1: Create Main Pluggable Database

### Objective
Create a permanent PDB for future class work with proper user configuration.

### Implementation

**PDB Name:** `jo_pdb_29181`  
**Username:** `jose_plsqlauca_29181`  
**Password:** `12345`

### Commands Executed
```sql
-- Connect as SYSDBA
CONNECT / AS SYSDBA

-- Create PDB
CREATE PLUGGABLE DATABASE jo_pdb_29181
ADMIN USER pdb_admin IDENTIFIED BY 12345
FILE_NAME_CONVERT = ('pdbseed', 'jo_pdb_29181');

-- Open PDB
ALTER PLUGGABLE DATABASE jo_pdb_29181 OPEN;

-- Verify PDB status
SHOW PDBS;

-- Switch to PDB
ALTER SESSION SET CONTAINER = jo_pdb_29181;

-- Create user
CREATE USER jose_plsqlauca_29181 IDENTIFIED BY 12345;

-- Grant privileges
GRANT CONNECT, RESOURCE, DBA TO jose_plsqlauca_29181;

-- Verify user
SELECT username FROM dba_users WHERE username = 'JOSE_PLSQLAUCA_29181';
```

### Evidence
![PDB Creation](screenshots/task1_pdb_creation.png)
![User Creation](screenshots/task1_user_creation.png)

---

## Task 2: Create and Delete Temporary PDB

### Objective
Demonstrate the ability to create and completely remove a PDB.

### Implementation

**Temporary PDB Name:** `jo_to_delete_pdb_29181`

### Commands Executed
```sql
-- Connect to root container
CONNECT / AS SYSDBA

-- Create temporary PDB
CREATE PLUGGABLE DATABASE jo_to_delete_pdb_29181
ADMIN USER temp_admin IDENTIFIED BY 12345
FILE_NAME_CONVERT = ('pdbseed', 'jo_to_delete_pdb_29181');

-- Open PDB
ALTER PLUGGABLE DATABASE jo_to_delete_pdb_29181 OPEN;

-- Verify it exists
SHOW PDBS;

-- Close PDB
ALTER PLUGGABLE DATABASE jo_to_delete_pdb_29181 CLOSE IMMEDIATE;

-- Delete PDB with datafiles
DROP PLUGGABLE DATABASE jo_to_delete_pdb_29181 INCLUDING DATAFILES;

-- Verify deletion
SHOW PDBS;
```

### Evidence
![Temporary PDB Created](screenshots/task2_temp_pdb_created.png)
![PDB Deleted](screenshots/task2_pdb_deleted.png)

---

## Task 3: Oracle Enterprise Manager (OEM)

### Objective
Access and demonstrate Oracle Enterprise Manager dashboard.

### Implementation

- **URL:** https://localhost:5500/em
- **Login:** SYSDBA
- **Dashboard Status:** Active and operational

### Evidence
![OEM Dashboard](screenshots/task3_oem_dashboard.png)

---

## Challenges Encountered and Solutions

### Challenge 1: ORA-65040 Error
**Issue:** Attempted to create PDB while connected to another PDB.  
**Solution:** Switched to CDB$ROOT using `CONNECT / AS SYSDBA` before creating PDBs.

### Challenge 2: Deleting Unwanted PDB (UW_PDB_29181)
**Issue:** Had an extra PDB that needed to be removed.  
**Solution:** Closed the PDB using `ALTER PLUGGABLE DATABASE CLOSE IMMEDIATE` and then dropped it with `DROP PLUGGABLE DATABASE INCLUDING DATAFILES`.

---

## Key Learnings

1. **Multitenant Architecture:** Understanding the relationship between CDB and PDBs
2. **Container Context:** Always verify which container you're connected to before executing commands
3. **PDB Lifecycle:** Creating, opening, closing, and dropping PDBs require specific privileges and container context
4. **User Management:** Users are created within specific PDBs and are isolated from other PDBs
5. **OEM Monitoring:** Oracle Enterprise Manager provides comprehensive visibility into database operations

---

## Academic Integrity Statement

I, **Jose (Student ID: 29181)**, hereby declare that:
- All work submitted in this assignment is my own
- All commands were executed individually on my own Oracle installation
- All screenshots are original and taken from my own database environment
- No AI tools, ChatGPT, or external assistance were used to generate commands or solutions
- No collaboration with classmates occurred during this assignment
- This work has not been copied or shared with others



---

## Repository Structure
```
oracle_pdb_ass_II_29181_jose/
├── README.md
└── screenshots/
    ├── task1_pdb_creation.png
    ├── task1_user_creation.png
    ├── task2_temp_pdb_created.png
    ├── task2_pdb_deleted.png
    └── task3_oem_dashboard.png
```

---

