# WAREHOUSE DATA DICTIONARY
---------------------------------------------------------------------------------------------------------------------------
Based on the ERD, attributes from the CourseData Database have been segregated into various tables. Each table and its attribute has been defined as follows:


**PROFESSORS_DW (Strong Entity)**
   - `Professor_id`: Acts as primary key for this table (and surrogate key when included in other tables)
   - `Name`: Name of the primary instructor teaching the course

**PROGRAMS_DW (Strong Entity)**
   - `Program_id`: Acts as primary key for this table (and surrogate key when included in other tables)
   - `program_code`: Abbreviation of the program names offered. Ex:program_code BU = 'Business' 
   - `program_name`: Names of the different subject streams offered at the university. Ex: Politics, Marketing, Mathematics

**LOCATIONS_DW (Strong Entity)**
   - `Location_id`: Acts as primary key for this table (and surrogate key when included in other tables)
   - `location`: Gives the location of the room in which the class will be held (format =  building name, room number). Ex: DSB 218 = Room 218 in the Dolan school of Business

**COURSES_DW (ID-Dependent Entity)**
   - `Course_id`: Acts as primary key for this table (and surrogate key when included in other tables)
   - `CatalogYear`: Identifies the year of the catalog
   - `Catalog_id`: Numeric code prefixed to the program code. May include a text identifier for specific programs. Ex: BI0352L, where L indicates "Lab'.
   - `Course_title`: Different course names offered under each program. Ex: 'Marketing' offers various courses such as 'Marketing Management', 'Customer Value', etc.
   - `Credits`: Number of credits offered by each course.
   - `Program_id`: Foreign key to PROGRAMS_DW
   
**TIMECODES_DW (Strong Entity)**
   - `Timecode_id`:
   - `Day`: Day of the week on which the class will be held.
   - `Start`: Date and start time of the class.
   - `End`: Date and end time of the class.
   

**CLASS_FACTS_DW (Fact Table)**
   - `Course_id`: Foreign key to COURSES_DW
   - `Program_id`: Foreign key to PROGRAMS_DW
   - `Offering_id`: 
   - `Location_id`: Foreign key to LOCATIONS_DW
   - `Professor_id`: Foreign key to PROFESSORS_DW
   - `Timecode_id`: Foreign key to TIMECODES_DW   
   - `CatalogYear`: Identifies the year of the catalog.
   - `Term`: Gives information about the semester in which the course is offered. Ex: Spring/Fall/Winter/Summer
   - `Credits`: Number of credits offered by each course.
   - `Section`: Indicates the section of the class.
   - `Cap`: Total number of students that can be enrolled in the course/ seats available for the course.
   - `Actual`: Total number of students enrolled in the course.
   - `Remaining`: Total number of seats remaining for course enrollment.
   - `Timecodes`: This column is a replica of meetings providing same information

  