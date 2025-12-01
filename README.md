# DW_Accesiones 

The Cubes created to analyze information are:

- Funding Sources

- OICRs

- MELIAs

- Innovations

- Policies

- Summary Indicators



# DW_Accesiones Github Structure
The structure is divided in three folders:

**ETLs:** ETLs folder has the pentaho Transformations and Jobs created to Extract, Transform and Load data from MARLO OLTP Application to MARLO BI Data warehouse (user marloBI)

**models:** models folder has the models for each cube in the data warehouse

**Tables:** Tables folder has the scripts used in the whole data warehouse creation process. They include staging tables, dimension tables and fact tables.

**ETLs Folder Structure:**

![image](https://user-images.githubusercontent.com/74072431/133151722-15165f15-f207-4378-aa05-7e19aec3b916.png)

ETLs folder is divided in the following sub-folders:

- 01dim: In this folder, you could find the pentaho transformations for dimensions: basic dimension, info dimensions and intersect dimensions. Info dimensions are all the dimension related to the fact, for example: dim_oicrs_info, dim_melias_info, dim_fs_info, and so on.

- 02stg: This folder contains the pentaho transformations related to staging tables. These transformations are intermediate ETLs and they participate in dimension and fact table  process. There are in there, the folowing sub-folders:

  - Deliverables, funding_sources, innovations, melias, milestone_status, milestones, oicrs, policies and projects: Transformations for specific dimension or table
  
  - generic: the transformatios for all staging tables related with generic dimensions
  
  - alliance: in this folder there are the transformations related to the Alliance CRIs.

   ![image](https://user-images.githubusercontent.com/74072431/133302171-ed2bac68-6366-4d05-88a1-27b7940d4dc4.png)


- 03fact: The folder has the pentaho transformations for the fact tables processes.

- 04job: In this folder could be found the pentaho jobs that execute the ETL processes. This folder has the following sub-folders:

  ![image](https://user-images.githubusercontent.com/74072431/133177664-40c1d12b-8b33-4cbe-b64e-d46f80a0172a.png)
   
  The folder has a few pentaho jobs that are the principal jobs to execute the process:
  
    - crp_BI_process.kjb: Executes the whole process. This pentaho job calls the following pentaho jobs:
    
      - 01_basic_dimensions_process.kjb: This job executes all the transformations related to basic dimensions
      
      - 02_info_dimensions_process.kjb: This job executes all the transformations related to info dimensions (i.e. dim_oicrs_info, dim_melias_info, etc)
      
      - 03_intersect_dimensions_process.kjb: This job executes all the transformations related to the intersect dimensions. Intersect dimensions have been created to deal with the many to many relationships between the fact tables and the dimensions.
                        
      - facts_process.kjb: This job executes the transformations to the fact tables process.
          

- 05misc: This folder has transformations for result dashboard process that could be useful in the MARLO-BI process

- config: This folder contains csv files for year, iso_alpha3 and general statuses. Also has the transformation to set the phase, which is used in some jobs.

**Tables Folder Structure:**

![image](https://user-images.githubusercontent.com/74072431/133155067-d73ad0f9-c87f-44db-974f-f49a2ac94aa5.png)

Tables folder has the folowing sub-folders:

- 01dim: This folder contains the sql scripts used to create dimension tables: basic dimension, info dimension an intersect dimension tables

- 02stg: This folder is used to store the sql creation  scripts for staging tables. There are the following sub-folders in there:

  - deliverables, funding_sources, innovations, melias, oicrs, policies and projects have the **staging tables** sql scripts for the staging info dimension tables

  - gendim sub-folder has the sql scripts about the **staging tables** for: basic dimensions and intersect dimensions.
  
  ![image](https://user-images.githubusercontent.com/74072431/133153557-7e268a1d-8fae-4074-9953-2e4eaab034c6.png)

  **Note:** deliverables folder has the staging tables for the existent deliverable table used for Deliverables Dashboard. Those tables will be replaced once the deliverables cube have been released.


- 03fact:This folder has the scripts for the fact tables

- 04misc: Inside this folder you could find the scripts to create process_log table and bi_phase_by_cubes table. bi_phase_by_cubes is created in the source schema to join the source tables.


# MARLO-BI How to execute the process

The process is executed using pentaho jobs and pentaho software: Pehtaho data integrator desktop or kitchen in command line mode.

The whole process use the crp_BI_process.kjb

![image](https://user-images.githubusercontent.com/74072431/133279667-156a202c-89e0-4641-b8f2-63dc0ed85dd9.png)

this job is in the folder:
MARLO-BI\ETLs\04job

In doppler server there is a shell file to execute the process using command line kitchen program: **create_crp_BI.sh**

located in **/home/doppler_admin/batchs/BI** folder /home/doppler_admin/batchs/BI








