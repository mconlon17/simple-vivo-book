# Preface

VIVO is a semantic web system for creating and maintaining an integrated view of the scholarly work of your organization.

As a semantic web application, VIVO uses an ontology to represent concepts.  It uses triples to express assertions about scholarship.  It uses RDF to represent those triples.  The triples constitute a graph of the data regarding your organization's scholarship. Finally, it uses a triple store to store the triples that constitute the graph.  All of these technologies (VIVO, ontology, triples, RDF, graph, and triple store) may be new to you and your organization.

Since 2009, VIVO has become available more broadly, and is now in use at more than 100 organizations world-wide.  The technologies it uses are still new to many, and can be very challenging.  Many data managers and traditional Information Technology departments have struggled to master the technologies, particularly those for entering and updating data in bulk.  Large organizations may have the manpower to commit to learning about the semantic web, building tools, deciphering VIVO's information representation models and eventually provide capabilities for bulk loading and managing their data.

Many organizations have developed custom solutions for what has become known as "the ingest" problem -- mapping traditional relational data sources to VIVO's graph models, and providing the means for adding, updating and removing data from VIVO based on authoritative sources of information such as the organization's human resource data, and the registrar's records of teaching.

Two existing solutions for the ingest problem should be noted.  1) The VIVO Harvester is a software tool that has been used by IT departments to perform VIVO data management from authoritative sources.  It requires professional IT staff and deep knowledge of the VIVO models. 2) Karma is an open-source, web-based tool that can be used to develop maps that allow data to be managed in web-based rectangles and uploaded to VIVO. Karma can be used by data managers who must master the VIVO data models to build Karma maps.

Despite its complexity and the dearth of data management tools, VIVO has prospered because it is open, and because its data model is extensible.  This extension capability is a blessing and a curse.  Extending the data model allows users of VIVO to represent any form of scholarship using any constructs they desire. The downside is that VIVO sites may diverge and become unable to share data, and standard tools for data management can not anticipate the diversity of extensions. 

Simple VIVO and is provided to fill a gap in VIVO data management practice.  Simple VIVO allows data managers to manage data from spreadsheets or any text editor capable of producing tab-delimited data, using standard VIVO data models.  Simple VIVO does not require mastering VIVO data models nor does it use any VIVO extensions.  Examples are provided for all the common elements of VIVO data management.  Using Simple VIVO you can create a VIVO from scratch, fill it with data about your scholarship, manage the data as it changes, and enjoy the benefits of VIVO -- open access to data regarding your scholarship, integrated data at the individual level for analysis, the ability to easily share your data with others, and presence in a growing community of scholars, data managers, and technologies working to create next generation scholarly ecosystems.

Managing data in VIVO was too difficult.  Only the most determined "early adopters" would commit to learning the underlying technologies, and the data models.  And only these early adopters would further develop their own custom methods for managing data in VIVO.  

With Simple VIVO, that has changed.  Simple VIVO provides the means for any group to manage VIVO data.  If you can use a spreadsheet and you understand basic concepts of data management, this book, and Simple VIVO, are for you.

We are trying to keep things simple.  If you find that some explanation is not clear, or some process is complex, please share your experience.

Two sets of examples are provided with Simple VIVO. 

The first set of examples, the "generic" examples, show how to use Simple VIVO to manage all elements of a VIVO profile in a scholarly organization without resort to additional software or VIVO extensions.  These examples should provide you with the means to manage your data in VIVO.

The second set of examples are from the University of Florida.  The University of Florida is one of the largest universities in the United States with more than 6,000 faculty, 50,000 students, and more than 950 academic and administrative departments.  Each year, the university teaches more than 12,000 courses, receives more than 3,000 grants, publishes more than 6,000 papers, and has more than 2,000 new employees.  Simple VIVO was designed to manage the data of the University of Florida.  University offices produce data on teaching, grants, and employment.  The examples provided with Simple VIVO show how data received from these offices can be managed in VIVO using Simple VIVO.  These examples use University of Florida ontology extensions.

I hope you find Simple VIVO useful.  And I hope to hear from you about your use of Simple VIVO.

[Mike Conlon](http://vivo.ufl.edu/individual/mconlon), Gainesville, Florida
