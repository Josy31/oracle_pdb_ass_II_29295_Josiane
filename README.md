Oracle Pluggable Database Assignment

1. Overview of Tasks

In this assignment, I worked with Oracle Pluggable Databases (PDBs). The practical work involved checking the Oracle database environment, creating a new PDB, opening it, switching between containers and later deleting a test PDB.

The main PDB I worked with was `jo_pdb_29295`.

Some of the activities I performed were:

- Checking the current container
- Viewing available PDBs
- Checking database file locations
- Creating `jo_pdb_29295`
- Opening the created PDB
- Switching from the root container to the PDB
- Checking the current user
- Deleting and recreating a PDB
- Creating another PDB for deletion practice
- Checking the PDBs after each important step

---

2. Oracle Environment Used

I used Oracle Database 21c XE for this practical assignment.

My Oracle database files were located in:

```text
C:\APP\KAYON\PRODUCT\21C\ORADATA\XE\
```

The main PDB created was:

```text
jo_pdb_29295
```

The administrator username used when creating it was:

```text
josiane_plsqlauca_29295
```

The environment also included the Oracle root container (`CDB$ROOT`) and the seed PDB (`PDB$SEED`)

3. Explanation of Tasks

Checking the Current Container

I first checked the container I was connected to using:

```sql
SHOW CON_NAME;
```

This helped me know whether I was working from the root container or inside a PDB.

Checking Available PDBs

I used the following command several times during the practical:

```sql
SHOW PDBS;
```

I mainly used it to check whether a PDB had been created, opened or deleted successfully.

Checking Data File Locations

Before creating the PDB, I checked the location of the Oracle data files.

```sql
SELECT FILE_NAME
FROM CDB_DATA_FILES
WHERE CON_ID = 2;
```

I also used:

```sql
SELECT file_name
FROM dba_data_files;
```

This helped me identify the path that I needed when using `FILE_NAME_CONVERT`.

Creating the PDB

I created my main PDB using:

```sql
CREATE PLUGGABLE DATABASE jo_pdb_29295
ADMIN USER josiane_plsqlauca_29295
IDENTIFIED BY <PASSWORD>
FILE_NAME_CONVERT = (
    'C:\APP\KAYON\PRODUCT\21C\ORADATA\XE\PDBSEED',
    'C:\APP\KAYON\PRODUCT\21C\ORADATA\XE\jo_pdb_29295'
);
```

The password is not shown in this README because it is private information.

After creating the PDB, I checked it using:

```sql
SHOW PDBS;
```

Opening the PDB

The new PDB needed to be opened before I could work inside it.

I used:

```sql
ALTER PLUGGABLE DATABASE jo_pdb_29295 OPEN;
```

Then I ran:

```sql
SHOW PDBS;
```

again to check its status.

Switching to the PDB

To start working inside the PDB, I changed the current container:

```sql
ALTER SESSION SET CONTAINER = jo_pdb_29295;
```

I confirmed the current container using:

```sql
SHOW CON_NAME;
```

I also checked the current user with:

```sql
SELECT USER FROM DUAL;
```

Correcting the PDB Setup

While doing the practical, I had an issue with the administrator username. I tried correcting the username with:

```sql
ALTER USER Josiane_plsqlquca_29295
RENAME TO josiane_plsqlauca_29295;
```

I later decided to remove the PDB and recreate it with the correct administrator username.

I first returned to the root container:

```sql
ALTER SESSION SET CONTAINER = CDB$ROOT;
```

Then I closed the PDB:

```sql
ALTER PLUGGABLE DATABASE jo_pdb_29295 CLOSE IMMEDIATE;
```

I removed it together with its data files:

```sql
DROP PLUGGABLE DATABASE jo_pdb_29295 INCLUDING DATAFILES;
```

I used `SHOW PDBS;` afterward to check that it had been removed.

### Recreating the Main PDB

I then recreated `jo_pdb_29295` with the correct administrator username:

```sql
CREATE PLUGGABLE DATABASE jo_pdb_29295
ADMIN USER josiane_plsqlauca_29295
IDENTIFIED BY <PASSWORD>
FILE_NAME_CONVERT = (
    'C:\APP\KAYON\PRODUCT\21C\ORADATA\XE\PDBSEED',
    'C:\APP\KAYON\PRODUCT\21C\ORADATA\XE\jo_pdb_29295'
);
```

After creating it, I opened it:

```sql
ALTER PLUGGABLE DATABASE jo_pdb_29295 OPEN;
```

I then checked the PDBs again using:

```sql
SHOW PDBS;
```

### Creating a PDB to Delete

I also created another PDB called `jo_to_delete_pdb_29295`.

```sql
CREATE PLUGGABLE DATABASE jo_to_delete_pdb_29295
ADMIN USER temp_admin
IDENTIFIED BY <PASSWORD>
FILE_NAME_CONVERT = (
    'C:\APP\KAYON\PRODUCT\21C\ORADATA\XE\PDBSEED',
    'C:\APP\KAYON\PRODUCT\21C\ORADATA\XE\jo_to_delete_pdb_29295'
);
```

I checked that it was created using:

```sql
SHOW PDBS;
```

I then deleted it using:

```sql
DROP PLUGGABLE DATABASE jo_to_delete_pdb_29295
INCLUDING DATAFILES;
```

Finally, I ran:

```sql
SHOW PDBS;
```

to check that the PDB was no longer available.

---

## 4. Challenges Faced

One problem I faced was with the administrator username. The username was not written correctly during part of the practical.

I first tried to correct the username, but I later removed the PDB and created it again using the correct administrator name `josiane_plsqlauca_29295`.

I also had to check the Oracle data file paths before creating the PDB because the correct paths were needed for `FILE_NAME_CONVERT`.

Using commands such as `SHOW PDBS` and `SHOW CON_NAME` helped me check my progress and know whether each operation had worked.

---

## 5. Integrity Statement

I confirm that the practical work documented in this repository represents the Oracle PDB tasks carried out for this assignment. The README explains the steps and SQL commands used during the practical work.

For security reasons, the database password used during the practical has not been included in this public repository.

---

## 6. Submission Details

```text
Repository Link: [GitHub URL]
PDB Name Created: jo_pdb_29295
Issues Encountered: Yes
```