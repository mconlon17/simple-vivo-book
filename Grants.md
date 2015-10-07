# Managing Grants

Grants are a bit more complex than some of the other entities we have been managing using Simple VIVO.  Grants
have the following columns:

1. Local award ID -- that is, what number, or other identifier, does your institution give this grant
1. Title -- the title of the grant.  This should be spelled out -- do not use abbreviations.  There is no length limit.
1. Direct costs -- all years -- a number without a dollar sign and with decimals as needed.  For example `43506.45`
1. Total award amount -- all years, direct plus indirect.  Same format as direct costs.
1. Principal investigators -- one or more principal investigators.  Investigators are specified using their orcid ID and separated by your intra field delimiter.
1. Co-principal investigators -- any number of co-principal investigators.  Specified using orcid, separated by intra field delimiter.
1. Investigators -- any number of investigators.  Specified using orcid, separated by intra field delimiter.
1. Concepts -- any number of concepts identifying subject areas for the grant.  Concepts are specified by name as they appear in the`concept-enum.txt` file. Concepts are separated by the intra field delimiter
1. Start date in the form yyyy-mm-dd
1. End date in the form yyyy-mm-dd
1. Administering unit.  Specified by name as they appear in `dept_enum.txt`
1. Sponsor.  Specified by name as they appear in `sponsor_enum.txt`
1. Sponsor's award ID -- how does the sponsor refer to this grant.  The National Institutes of Health in the US, for
example, gives its grants award ID that look like R01DK22343
1. URI in VIVO.  Blank if you are adding the grant.  VIVO URI returned by get.

## Enumerations

Simple VIVO for grants uses several enumerations to identify data in VIVO.  Each enumeration is made by`make_enum.py` 
as described below.

1. `concept_enum.txt` lists the concepts in your VIVO by name
1. `date_enum.txt` lists the year-month-day dates in your VIVO by date value
1. `dept_enum.txt` lists your institutions organizations by name
1. `orcid_enum.txt` lists your investigators by ORCID.  ORCID is used to identify your investigators.  
Each should have an ORCID, and the ORCID for each investigator should be in your VIVO.  See examples/people for
adding ORCID to people.
1. `sponsor_enum.txt` lists the sponsors (funding organizations) in your VIVO.

Each attribute is optional.  You may add a grant with very little information and provide improved values for attributes in subsequent updates.

As always, your spreadsheet values will be non-blank if you would like to specify a value for the attribute, blank if you would like to have VIVO remain unchanged, and "None" if you would like to remove the attribute's value from VIVO.

## The Basic steps

1. Use `make_enum.py` to prepare the enumerations for grants

    `python make_enum.py``

1. Use get to retrieve the grants from your VIVO to a spreadsheet

    `python sv.py -a get`
    
1. Edit your spreadsheet to improve your grant data, and add new grants

1. Use update to put your improved grant data back in VIVO

    `python sv.py -a update`
    
1. Repeat the steps each time you wish to improve your grant data

