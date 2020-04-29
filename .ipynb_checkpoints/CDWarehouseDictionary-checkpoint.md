# DATA DICTIONARY
---------------------------------------------------------------------------------------------------------------------------
Based on the ERD, each attributes in the 3 csv files (CourseCatalog, Courses and Course meetings) have been segregated into various tables. Each table and its attribute has been defined as follows:


**PROFESSORS (Strong Entity)**
   - `Professor_id`: Acts as primary key for this table (and surrogate key when included in other tables)
   - `Name`: Name of the primary instructor teaching the course

**PROGRAMS (Strong Entity)**
   - `Program_id`: Acts as primary key for this table (and surrogate key when included in other tables)
   - `program_code`: Abbreviation of the program names offered. Ex:program_code BU = 'Business' 
   - `program_name`: Names of the different subject streams offered at the university. Ex: Politics, Marketing, Mathematics

**LOCATIONS (Strong Entity)**
   - `Location_id`: Acts as primary key for this table (and surrogate key when included in other tables)
   - `location`: Gives the location of the room in which the class will be held (format =  building name, room number). Ex: DSB 218 = Room 218 in the Dolan school of Business

**COURSES (ID-Dependent Entity)**
   - `Course_id`: Acts as primary key for this table (and surrogate key when included in other tables)
   - `CatalogYear`: Identifies the year of the catalog
   - `Catalog_id`: Numeric code prefixed to the program code. May include a text identifier for specific programs. Ex: BI0352L, where L indicates "Lab'.
   - `Course_title`: Different course names offered under each program. Ex: 'Marketing' offers various courses such as 'Marketing Management', 'Customer Value', etc.
   - `Credits`: Number of credits offered by each course.
   - `Attributes`: Indicates whether the course fulfills the university requirement. Ex: US Diversity, World Diversity.
   - `Prereqs`: Indicates whether the course requires any specific pre-requisite before enrolling
   - `Coreqs`: Indicates which course a student must take at the same time as a specific course, if applicable
   - `Description`: Provides a decsription of the details and the outcomes of the course
   - `Fee`: Fee charged by specific courses for providing additional course material/use of lab equipment/private lessons
   - `Program_id`: Foreign key to PROGRAMS
   
**COURSE_OFFERINGS (ID-Dependent Entity)**
   - `Offering_id`: Acts as primary key for this table (and surrogate key when included in other tables).
   - `CatalogYear`: Identifies the year of the catalog.
   - `Term`: Gives information about the semester in which the course is offered. Ex: Spring/Fall/Winter/Summer
   - `Section`: Indicates the section of the class.
   - `CRN (Course Reference Number)`: Unique numeric specifier to identify the course.
   - `Title`: Different course names offered under each program. Ex: 'Marketing' offers various courses such as 'Marketing Management', 'Customer Value', etc.
   - `Credits`: Number of credits offered by each course.
   - `Cap`: Total number of students that can be enrolled in the course/ seats available for the course.
   - `Actual`: Total number of students enrolled in the course.
   - `Remaining`: Total number of seats remaining for course enrollment.
   - `Meetings`:  Calendar duration, time, day and location of the class being held.
   - `Timecodes`: This column is a replica of meetings providing same information
   - `Course_id`: Foreign key to COURSES
   - `Professor_id`: Foreign key to PROFESSORS
   
**MEETINGS (ID-Dependent Entity)**
   - `Meetings_id`: Acts as primary key for this table (and surrogate key when included in other tables).
   - `Day`: Day of the week on which the class will be held.
   - `Start`: Date and start time of the class.
   - `End`: Date and end time of the class.
   - `Location_id`: Foreign key to LOCATIONS
   - `Offering_id`: Foreign key to COURSE_OFFERINGS
   
**CATALOG_YEAR (ID-Dependent Entity)**
   - `CatalogYear`: Identifies the year that the class' catalog was published
   - `Term`: Gives information about the semester in which the course is offered. Ex: Spring/Fall/Winter/Summer
  