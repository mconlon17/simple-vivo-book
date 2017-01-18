# Managing Memberships

People have memberships in organizations.  People may be chairs or members of committees, or have memberships in professional organizations.  Memberships have date ranges.  All of these can be represented by VIVO memberships using the techniques described below.

Memberships have five attributes:

1. Start date -- when did the membership start? From an enumeration of dates of the form yyyy-mm-dd
2. End Date -- when did the membership end?  Leave blank if the membership is on-going.  From an enumeration of dates of the form yyyy-mm-dd
3. Organization of Membership -- from an enumeration of organizations by name
4. Person in position -- from an enumeration of people by name
5. Membership role -- open text.  Typically "Member" or "Chair."

## The steps to manage memberships

1. Update your enumerations using `python make_enum.py`
2. Get memberships from your VIVO using `python sv.py -a get`
3. Edit your spreadsheet `membership.txt` correcting and adding information for existing memberships,
   and adding new memberships.  Use a text editor or spreadsheet program
4. Update the membership information in your VIVO using `python sv.py -a update`

Repeat the steps as necessary.

