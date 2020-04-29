# BA 510 Course Data Project
__Spring 2020__

Team Cornertable
Archana Agarwal
James Finnegan
Elise Vincent

## Introduction
For our semester project, Team Cornertable produced a database and a data warehouse utilizing raw data collected from Fairfield Univerity's course catalog, semester schedules, and academic calendar.  The data files that we used to populate our database and data warehouse were csv files that provided information including: course offerings, course meetings, and program details.  As mentioned, this data was used to populate a relational database (Coursedatabase.db) and data warehouse (CourseDataWarehouse.db).  Throughout this project we applied knowledge of the course objectives in the following ways:

- Translating and documenting the data through the creation of an ERD which we used to structure and design our database (Coursedata.db)
- Uploading the data (csv files) and populating the database
- Testing our database to ensure domain, entity, and relational integrity (CourseDataTests - FINAL.ipynb)
- Creation of a data warehouse (DataWarehouse.db) in a star-schema format
- Testing our data warehouse to ensure domain, entity, and relational integrity (CourseDataWarehouseTests - FINAL.ipynb)
- Querying our database/data warehouse in order to answer key questions and demonstrate the efficiency and usefulness of our data warehouse  (WarehouseUtilization_Done.ipynb)


## Step 1 - ERD

The data from the csv files was used to build our Entity Relationship Diagram (ERD).  The ERD is essentially a diagram that allows us to visualize not only the tables, but also the relationships between the tables.  The SourceData folder includes folders for each semester, and each folder includes two csv files (courses.csv and course_meetings) that provides raw data including courses offerings, course meetings, and program details.  The Catalogs folder contains two additional csv files that provide information related to the different programs offered at Fairfield University.

- courses.csv: includes specific details around classes offered at Fairfield University with meeting details for each term.  The columns included are term, crn, catalog_id, section, credits, title, meetings, timecodes, primary_instructor, cap, act, and rem.

- course_meetings.csv: includes specific details around courses and meetings.  The columns included are crn, location, day, start, and end. 

- CourseCatalog2017_2018.csv and CourseCatalog2018_2019.csv: columns included are program_code, program_name, catalog_id, course_title, dredits, prereqs, coreqs, fees, attributes, description.

After becoming familiar with these files, we constructed our CourseDataERD.pdf file, and you can see our detailed description of each column in our CourseDataDictionary - Final.md file.


At a high-level, our ERD is designed as follows:

- COURSES: Fairfield University course information from the course catalogs
- COURSE OFFERINGS: data that is unique to class (namely when it is offered)
- PROGRAMS: information about the programs (subjects) that the courses are related to
- PROFESSORS: faculty or instructor information
- MEETINGS: data that describes the time each class meets
- LOCATIONS: where the classes take place



## Step 2 - Creating the database file

The next step in our process was to create tables in the CourseData.db file from the entities we laid out in our ERD.  This is the creation of our database file, where we drop tables and create the columns detailed in our ERD.  You may reference the code we wrote, cells 4-9, in the CourseDataETL_Done.ipyn file.


## Step 3 - Importing Data

The third step was this import the raw data into the database, which we accomplished using Professor Huntley's suggested Python coding, which is detailed between cells 12 and 14 in the CourseDataETL_Done.ipyn file.  After completing this, we checked the data for duplication in cells 15 - 17.


# Step 4 - Testing Integrity

Our team created a new notebook, CourseDataTests - FINAL.ipynb, to test the integrity of our database.  This file contains each of the queries we wrote to check:

- Domain integrity: the allowed values of an attribute determine domain integrity, definitions include data type, length, range or constraints.  This test was completed in cells 3 and 4.  Here we ran SELECT queries to determine that the number of records in each table made sense (CatalogCourses, CourseOfferings, and CourseMeetings).  

- Entity integrity: testing to ensure that each object represented by a row in the table should be distiguishable from any other object.  SELECT queries where again utilized to ensure that we successfully retrieved unique values for Professors, Programs, Locations, Courses, Course Offerings, and Meetings (cells 5-10).

      
- Relational integrity: testing to ensure that table relationships are consistent, or that any foreign key field must agree with the primary key that is referenced by the foreign key (cells 11-16).  We wrote queries (utilizing JOINs) testing:
    Does Catalog_ID make sense with Program_Code & Program_Name?
    Confirming that Professor Lane teaches Economics and Finance
    Check that Title and Course_Title are the same
    Check that Day, Start, End match Meetings


# Step 5 - Design and Build Data Warehouse

The fifth step was to design a data warehouse, which we saved as CourseDataWarehouse.db. We utilized a star schema design to construct our data warehouse with CLASS_FACTS_DW as our facts table. From there, we constructed five dimension tables:

1. COURSES_DW, containing:
    course_id
    CatalogYear
    catalog_id
    course_title
    credits
    program_id 
    
2. TIMECODES_DW, containing:
    timecode_id
    day
    start
    end
    
3. PROGRAMS_DW, containing:
    program_id
    program_code
    program_name
    
4. PROFESSORS_DW, containing:
    professor_id
    name

5. LOCATIONS_DW, containing:
    Location_id
    Location 
    
Our ERD, written in a star schema, is located in the ERD for data warehouse2.pdf file.  


Once the ERD was created, we then built the data warehouse (CourseDataWarehouse.db), our process documented in the CourseDataWarehouseETL_Done notebook.  The dimension tables were contructed and populated first, followed by our fact table (CLASS_FACTS_DW).


# Step 6 - Test CourseDataWarehouse.db for data integrity

This step was completed in the same manner as our database file, testing for Domain, Entity and Relational integrity.  This is detailed in our file CourseDataWarehouseTests.ipynb



# Step 7 - Demo your results with useful queries

Our questions include the following (found in WarehouseUtilization_Done.ipynb):

1) Which program has the most courses? The least?
2) Which classroom is the most utilized, and what programs hold classes there?
3) Which classes go over capacity the most frequently? 
4) Which professors has the most diverse courseload?
5) Which professor teaches in the highest number of programs?
6) Which days are the most/least popular for classes?
7) Which classes are attracting less than 10 students? (> 0)



# Step 8 Deliver a walkthrough presentation of your work

This readme.md file with serve as the guide for our work this semester, including a link to each of the files we will be reviewing.  Thank you very much for the opportunity to share this with you!

- Team Cornertable
