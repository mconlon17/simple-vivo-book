# Managing Teaching in Simple VIVO

To manage teaching in Simple VIVO, you will need to manage a list of courses, and you will need to specify 
teaching -- who taught what when.

Each is described below.

## Courses

Managing a list of courses is easy.  Courses have two columns -- the name of the course and the concepts of the 
course.  If your courses have course numbers, you may want to include them in the name of the course.  So, for 
example, if the name of
your course is "Introduction to Statistics" and the course number is "STA 1201," you may want to have the name in 
VIVO be "STA 1201 Introduction to Statistics"

You can use:

    python -a get -c sv_courses.cfg -s courses.txt
    
to get a spreadsheet of the courses you have in VIVO.  Add the names of courses, or edit the names as needed,
and then update your list in VIVO using:

    python -a update -c sv_courses.cfg -s courses.txt
    
## Teaching

To manage teaching, you will need a list of courses in VIVO (see above).

For each course taught by an instructor, you will need to know:

1. The course that was taught -- by name of the course
1. The person who taught the course -- by orcid 
1. The start date for the course -- year month day by value
1. The end date for the course -- year month day by value.  For example "2015-12-09"

You can use:

    python make_enum.py

to prepare the enumerations for your work.  Then use:

    python sv.py -a get

to get a spreadsheet of your courses.  Add to it, edit, remove as needed.

You can then use:

    python sv.py -a update

to update VIVO to include your changes.

Repeat these four steps -- make_enum, get, edit, update -- whenever you would like to edit your teaching records.