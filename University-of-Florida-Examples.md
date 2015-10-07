# University of Florida Examples

The University of Florida (UF) uses the Pump and Simple VIVO to manage its enterprise VIVO.  Both the Pump and Simple VIVO were developed at UF to meet the need of upgrading VIVO from the 1.5 ontology to versions of VIVO supporting the 1.6 ontology (VIVO software version 1.6 and above).  The University had tens of thousands of lines of code that were dependent on the 1.5 ontology -- code that put data into VIVO and code that took data out of VIVO.  These two basic functions became the update and get functions that we see in the Pump and Simple VIVO.

The University of Florida examples have several characteristics that distinguish them from the previous Simple VIVO examples:

1.  The examples are large scale.  UF is a large institution with over 900 institutional organizations, 6,000 faculty, and approximately 6,000 publications and 2,00 new grants per year.
1.  The examples demonstrate the clean-up of enterprise data for display in VIVO.  Like most institutions, the data of the University of Florida is optimized for internal transactional processing.  It was never intended for integrated, external display of the scholarly work of the organization.  Much effort has been put into preparing for integration and display of the scholarly work.
1.  The examples use data source external to the organization.  Examples show the use of PubMed and other external sources to augment the institution's data.
1. The examples make use of ontology extensions.  UF finds it convenient to extend the ontology for several purposes -- to better represent its work, and to provide local identifiers for entities in VIVO.

## The UF domains

1. Orgs
    * Organization data management -- management via spreadsheet.  No institutional data
1. People
    * Ensure UF business rules
    * Manage UFCurrentEntity
    * Support excluding people from automated edited
1. Position Management
    * Support UF terminology and business rules
    * Exclude positions in protected departments
    * Improve position titles
    * Manage types
1. Papers
    * Ingest from PubMed IDs
    * Ingest from DOI
    * Ingest from CSV (bibTex to CSV)
1. Courses
    * Include common course number.  Serve as the abstraction layer for course sections, much as awards have AwardReceipt and Award, and degrees have AwardedDegree and AcademicDegree, UF recognizes CourseSection (as taught) and Course (model).
1. Course Sections
    * Link to courses, instructors, terms
1. Sponsors
    * With UF sponsorid
1. Grants
    * Linked to departments, datetimes, cois, pis, invs
