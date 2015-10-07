# Managing Positions Using Simple VIVO

People have positions in organizations.  Some positions are "official" -- a person is employed with a job title
such as "Professor" or "Research Assistant."  Some positions may be "official" but unpaid -- a person may be
director of a center or president of a professional society.  Some positions may be unofficial -- a person may be
an evaluation lead for a program.  All of these can be represented using VIVO positions using the techniques
described below.

Positions have five attributes:

1. Start date -- from an enumeration of dates of the form yyyy-mm-dd
1. End Date -- from an enumeration of dates of the form yyyy-mm-dd
1. Organization of Position -- from an enumeration of organizations by name
1. Person in position -- from an enumeration of people by orcid
1. Job title -- open text

## The steps to manage positions

1. Update your enumerations using `python make_enum.py`
1. Get positions from your VIVO using `python sv.py -a get`
1. Edit your spreadsheet `positions.txt` correcting and adding information for existing positions,
and adding new positions.  Use a text editor or spreadsheet program
1. Update the position information in your VIVO using `python sv.py -a update`

Repeat the steps as necessary.  