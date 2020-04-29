# BA 510 Course Data Project
__Spring 2020__

## Team Cornertable
- Archana Agarwal
- James Finnegan
- Elise Vincent

## Introduction
For our semester project, Team Cornertable produced a database and a data warehouse utilizing raw data collected from Fairfield Univerity's course catalog, semester schedules, and academic calendar.  The data files that we used to populate our database and data warehouse were csv files that provided information including: course offerings, course meetings, and program details.  As mentioned, this data was used to populate a relational database (Coursedatabase.db) and data warehouse (CourseDataWarehouse.db).  Throughout this project we applied knowledge of the course objectives in the following ways:

- Translating and documenting the data through the creation of an ERD which we used to structure and design our database (Coursedata.db)
- Uploading the data (csv files) and populating the database
- Testing our database to ensure domain, entity, and relational integrity (CourseDataTests - FINAL.ipynb)
- Creation of a data warehouse (DataWarehouse.db) in a star-schema format
- Testing our data warehouse to ensure domain, entity, and relational integrity (CourseDataWarehouseTests - FINAL.ipynb)
- Querying our database/data warehouse in order to answer key questions and demonstrate the efficiency and usefulness of our data warehouse  (WarehouseUtilization_Done.ipynb)


## Step 1 - ERD

The data from the csv files was used to build our Entity Relationship Diagram (ERD) to allow us to visualize the tables and the relationships between the tables. The SourceData folder includes folders for each semester, and each folder includes two csv files (`courses.csv` and `course_meetings`) that provides raw data including course offerings, course meetings, and program details.  The Catalogs folder contains two additional csv files that provide information related to the different programs offered at Fairfield University.

- courses.csv: includes specific details around classes offered at Fairfield University with meeting details for each term.  The columns included are term, crn, catalog_id, section, credits, title, meetings, timecodes, primary_instructor, cap, act, and rem.

- course_meetings.csv: includes specific details around courses and meetings.  The columns included are crn, location, day, start, and end. 

- CourseCatalog2017_2018.csv and CourseCatalog2018_2019.csv: columns included are program_code, program_name, catalog_id, course_title, dredits, prereqs, coreqs, fees, attributes, description.

Using our general knowledge and Fairfield's course catalogs, we constructed a [Dictionary](https://github.com/fairfield-ba510-spring2020/term-project-cornertable/blob/master/CourseDataDictionary.md) to define each column, including the foreign keys we would introduce. After becoming familiar with these files, we constructed our [ERD](https://github.com/fairfield-ba510-spring2020/term-project-cornertable/blob/master/CourseDataERD.pdf) file.

At a high-level, our ERD is designed as follows:

- COURSES: Fairfield University course information from the course catalogs
- COURSE OFFERINGS: data that is unique to class (namely when it is offered)
- PROGRAMS: information about the programs (subjects) that the courses are related to
- PROFESSORS: faculty or instructor information
- MEETINGS: data that describes the time each class meets
- LOCATIONS: where the classes take place



## Step 2 - Creating the database file

The next step in our process was extract, transform and load the data from the given csv files into a [database](https://github.com/fairfield-ba510-spring2020/term-project-cornertable/blob/master/CourseDataETL.ipynb) joined in a manner consistent with our ERD.
1. Loading the SQL extension
2. Using DROP TABLE/ CREATE TABLE commands to add tables to our database - first the strong entities (PROFESSORS,PROGRAMS,LOCATIONS), then the weak entities (COURSES,COURSE_OFFERINGS) using appropriate foreign keys.
3. Create Catalog_Year table to extract `Term` and `CourseYear`for easy term differentiation.
4. Import csv files and confirm row count (note duplicate issue in course_meetings.csv)
5. Use DELETE FROM/INSERT INTO commands to move data from the corresponding datasets into each table. We did this in the the same order table creations (strong, then weak) to minimize any potential JOIN issues
6. Drop the CSV datasets and vacuum data to resolve storage issues.


# Step 3 - Testing Integrity

Our team created a [testing notebook](https://github.com/fairfield-ba510-spring2020/term-project-cornertable/blob/master/CourseDataTests.ipynb) to test the integrity of our database.  This file contains each of the queries we wrote to check:

- Domain integrity: the allowed values of an attribute determine domain integrity, definitions include data type, length, range or constraints. Here we ran SELECT queries to determine that the number of records in each table made sense (CatalogCourses, CourseOfferings, and CourseMeetings).  

- Entity integrity: testing to ensure that each object represented by a row in the table should be distiguishable from any other object.  SELECT queries where again utilized to ensure that we successfully retrieved unique values for Professors, Programs, Locations, Courses, Course Offerings, and Meetings.

      
- Relational integrity: testing to ensure that table relationships are consistent, or that any foreign key field must agree with the primary key.  We wrote queries (utilizing JOINs) testing:
- Does Catalog_ID make sense with Program_Code & Program_Name?
- Confirming that Professor Lane teaches Economics classes
- Check that Title and Course_Title are the same
- Check that Day, Start, End match Meetings


# Step 4 - Design and Build Data Warehouse

The fifth step was to design an [ERD for our data warehouse](https://github.com/fairfield-ba510-spring2020/term-project-cornertable/blob/master/CourseDataWarehouseERD.pdf). We utilized a star schema design to construct our data warehouse with CLASS_FACTS_DW as our facts table. To extract transform and load data from our CourseData Database into our [data warehouse](https://github.com/fairfield-ba510-spring2020/term-project-cornertable/blob/master/CourseDataWarehouseETL.ipynb) we constructed five dimension tables along with our fact table:

1. COURSES_DW, containing:
    course_id, 
    CatalogYear, 
    catalog_id, 
    course_title, 
    credits, 
    program_id
    
2. TIMECODES_DW, containing:
    timecode_id, 
    day, 
    start, 
    end
    
3. PROGRAMS_DW, containing:
    program_id, 
    program_code, 
    program_name
    
4. PROFESSORS_DW, containing:
    professor_id, 
    name

5. LOCATIONS_DW, containing:
    Location_id, 
    Location 
    
6. COURSE_FACTS_DW, containing:
    Course_id,  
    Program_id,  
    Location_id, 
    Professor_id,  
    Offering_id,  
    Timecode_id, 
    CatalogYear, 
    Term, 
    Credits, 
    Section,  
    Cap, 
    Actual, 
    Remaining, 
    Timecodes, 
    Count_courses, 
    Num_students, 
    Count_location

We followed similar steps to create our Warehouse:

1. Loading the SQL extension and connecting SQLite to the warehouse
2. Using DROP TABLE/ CREATE TABLE commands to add tables- first the strong entities (PROFESSORS_DW,PROGRAMS_DW,LOCATIONS_DW), then the weak entities (COURSES_DW,COURSE_OFFERINGS_DW) with foreign keys, followed last by the joint COURSE_FACTS_DW TABLE.
3. As we were joining the tables, we constructed a help table to allow for easier access to the class start and end times (not a string with date/time)
4. Use DELETE FROM/INSERT INTO commands to move data from the corresponding datasets into each warehouse table. We did this in the the same order table creations (strong, then weak) to minimize any potential JOIN issues
5. Vacuum data to resolve storage issues.


# Step 5 - Test CourseDataWarehouse.db for data integrity

[This step](https://github.com/fairfield-ba510-spring2020/term-project-cornertable/blob/master/CourseDataWarehouseTest.ipynb) was completed in the same manner as our database file, testing for Domain, Entity and Relational integrity.



# Step 6 - Demo your results with useful queries

We designed our warehouse with the idea that University administrators and deans- those who are responsible for monitoring program attendance faculty courseload, classroom and course availability. It would be providing an organizational view of information needed to run and understand the university programming. [Our questions](https://github.com/fairfield-ba510-spring2020/term-project-cornertable/blob/master/CourseDataWarehouseDemo.ipynb) include the following:

1. On which day are the most/least classes held?
2. Which classroom is the most utilized, and what programs hold classes there?
3. Which professors has the most diverse courseload?
4. Which professor teaches in the highest number of programs?
5. Which program has the most/least amount of courses?
6. Which classes go over capacity the most frequently? 
7. Which classes are attracting less than 10 students?

