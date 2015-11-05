# Managing Awards and Honors using Simple VIVO

For Awards and Honors, VIVO distinguishes between two ideas:

1.  The generic award (as in the Nobel Peace Prize)
2.  And the instance of the award as in "Theodore Roosevelt won the Nobel Peace Prize in 1906"

This allows us to easily list all the people who won any particular award.

To add awards and honors to VIVO, we need to know several pieces of information for each award or honor:

1. Who got the award or honor?  e.g. Theodore Roosevelt
1. What award or honor was received?  e.g. Nobel Peace Prize
1. From what organization?  e.g. Norwegian Nobel Committee
1. What is the date of the award? e.g. 1906

Each of these four things "Theodore Roosevelt", "Nobel Peace Prize," "Norwegian Nobel Committee," and the date 1906 must all be in VIVO *before* the indication of the award to Roosevelt can be added by Simple VIVO.  Adding Awards and Honors makes the links between these four things, not the things themselves.

## Managing Enumerations

Each of the four things is represented by an enumeration:

1. person_enum for who
1. award_enum for what
1. org_enum for where
1. date_enum for when

The python program `make_enum.py` can be used to update these enumerations using data from your VIVO.  To run 
`make_enum.py` use:

    python make_enum.py
    
## Managing Awards

Once the things to be talked about are in VIVO, and the enumerations are made, you can use 

    python sv.py -a get
    
to get the awards and honors from your VIVO into a spreadsheet called `awards.txt`  You can add awards to your spreadsheet being sure to use values from each of your enumerations.

Once you have awards to add to VIVO, use:

    python sv.py -a update
    
which will create the `award_add.rdf` and `award_sub.rdf` to update your VIVO.

## Adding People, Awards, Dates, and Organizations to your VIVO

To manage awards, your enumerations must be up to date.  Each person, organization, award, and date that will be referenced in an award must already be in  your VIVO and in your enumerations.  Updating your enumerations is simple -- run `make_enum.py` as shown above.

If you need to add dates, rerun the dates example with a wider date range.

To add a single person, name of an award, or an organization conferring an award, use the VIVO web interface.  Update
the enumerations, add a row to your `awards.txt` for the new award and run a Simple VIVO update.  

For example:

John Smith earns a lifetime achievement award from the American Cancer Society in 2015.  John Smith and the date 2015 are already in your VIVO, but the American Cancer Society and the lifetime achievement award are not.

1. Use the Site Admin interface to add the American Cancer Society as an organization.

1. Use the Site Admin interface to add "ACS Lifetime Achievement Award" as an award.

1. Update the enumerations.  Now all four elements of the award receipt (person, date, award and organization) are in your VIVO and in your enumerations. You can add a row to your `awards.txt` spreadsheet that looks like

    `John Smith  ACS Lifetime Achievement Award  American Cancer Society 2015`
    
1. Run `python ../../sv.py -a update`
    and the award will be in place.



