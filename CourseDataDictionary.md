# DATA DICTIONARY
---------------------------------------------------------------------------------------------------------------------------
Based on the ERD, each attributes in the 3 csv files (CourseCatalog, Courses and Course meetings) have been segregated into various tables. Each table and its attribute has been defined as follows:


**PROFESSORS (Strong Entity)**
   - `Professor_id`: It is the primary key and the surrogate key for the table to join it with other table.
   - `Name` - Name of the primary instructor teaching the course.

**PROGRAMS (Strong Entity)**
   - `Program_id`: It is the primary key and the surrogate key for the table to join it with other table.
   - `program_code`: Abbreviation of the program names offered. Ex:program_code BU means 'Business' which is one of the program names offered.
   - `program_name`: Names of the different subject streams offered at the university. Ex: Politics, Marketing, Mathematics

**LOCATIONS (Strong Entity)**
   - `Location_id`: It is the primary key and the surrogate key for the table to join it with other table.
   - `location`: Gives the location of the room in which the class will be held. It is combination of the building name followed by the room number in that building. Ex: DSB 218 means Room 218 in the Dolan school of business.

**COURSES (ID-Dependent Entity)**
   - `Course_id`: It is the primary key and the surrogate key for the table to join it with other table.
   - `CatalogYear`: Identifies the year of the catalog.
   - `Catalog_id`: Numeric code prefixed to the program code. May include a text identifier for specific programs. Ex: BI0352L, where L indicates "Lab'.
   - `Course_title`: Different course names offered under each program. Ex: 'Marketing' offers various courses like 'Marketing Management', 'Customer Value', etc.
   - `Credits`: Number of credits offered by each course.
   - `Attributes`: Indicates whether the course fulfills the university requirement. Ex: US Diversity.
   - `Prereqs`: Defines if a particular course requires any specific pre-requisite/requirement for enrolling in the course or not.
   - `Coreqs`: It means a course or other requirement that a student must take at the same time as another course or requirement.
   - `Description`: It gives a rough decsription about the details and the outcomes of the course.
   - `Fee`: Fee charged by specific courses for providing additional course material/use of lab equipment and private lessons.
   - `Program_id`: It is the foreign key to the table.
   
**COURSE_OFFERINGS (ID-Dependent Entity)**
   - `Offering_id`: It is the primary key and the surrogate key for the table to join it with other table.
   - `CatalogYear`: Identifies the year of the catalog.
   - `Term`: It gives information about the period in which the course is offered. Ex: Spring/Fall/Winter/Summer
   - `Section`: Indicates the section of the class.
   - `CRN (Course Reference Number)`: Unique specifier for identify the course.
   - `Title`: Different course names offered under each program. Ex: 'Marketing' offers various courses like 'Marketing Management', 'Customer Value', etc.
   - `Credits`: Number of credits offered by each course.
   - `Cap`: Total number of students that can be enrolled in the course/ seats available for the course.
   - `Actual`: Total number of students enrolled in the course.
   - `Remaining`: Total number of seats remaining for the course enrollment.
   - `Meetings`:  Provides combination of 4 keys i.e. date, time, day and location of the class being held.
   - `Timecodes`: This column is a replica of meetings providing same information in a more refined format.
   - `Course_id`: It is the foreign key to the table.
   - `Catalog_id`:It is the foreign key to the table.
   - `Professor_id`: It is the foreign key to the table.
   
**MEETINGS (ID-Dependent Entity)**
   - `Meetings_id`: It is the primary key and the surrogate key for the table to join it with other table.
   - `Day`: Day of the week on which the class will be held.
   - `Start`: Date and start time of the class.
   - `End`: Date and end time of the class.
   - `Location_id`: It is the foreign key to the table.
   - `Offering_id`: It is the foreign key to the table.
   
**CATALOG_YEAR (ID-Dependent Entity)**
   - `CatalogYear`: Identifies the year of the catalog.
   - `Term`: It gives information about the period in which the course is offered. Ex: Spring/Fall/Winter/Summer
  