**Student Name:** Uwase Rubagumya Jose 
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
(<img width="422" height="77" alt="Screenshot 2026-02-15 183300" src="https://github.com/user-attachments/assets/c0cacbe2-2cfa-444e-83e0-c2ec5b66bf95" />
![PDB open state](https://github.com/user-attachments/assets/0f21db98-aee4-456c-8090-deef317d6a82)
![User created](https://github.com/user-attachments/assets/a6efe621-3472-437b-b73a-9aa272eccb4b)

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

![tempory](https://github.com/user-attachments/assets/93e7579a-813c-4078-a41f-95e424593698)
![VERIFY](https://github.com/user-attachments/assets/1fa28299-6325-4907-aa33-eaa0319e5107)
![Delect PDB](https://github.com/user-attachments/assets/46fdccf3-253e-48e7-9d42-0453ea719da8)
![TEMPORARY  PDB exist](https://github.com/user-attachments/assets/69cca188-8285-485b-9d0c-adf134ab2151)

---

## Task 3: Oracle Enterprise Manager (OEM)

### Objective
Access and demonstrate Oracle Enterprise Manager dashboard.

### Implementation

- **URL:** https://localhost:5500/em
- **Login:** SYSDBA
- **Dashboard Status:** Active and operational

### Evidence
![OEM Dashboard](![OEM dashboard](https://github.com/user-attachments/assets/52ff5c16-cf8a-492e-854d-8df560a6c82d)


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

I, **UWASE RUBAGUMYA Josee (29181), declare that this assignment is my own work.

All commands were executed by me in my Oracle Database, and all screenshots are original.

I have not copied from or collaborated with anyone.

This assignment reflects my knowledge and work in managing Oracle Pluggable Databases (PDBs), including resolving naming issues when they arose.



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

