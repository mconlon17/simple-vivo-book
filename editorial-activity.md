# Managing editorial activities in Simple VIVO

Editorial activities such as editor, associate editor, assistant editor, or reviewer of a journal have five attributes:

1. Start date for the activity -- from an enumeration of dates of the form yyyy-mm-dd

2. End date for the activity -- from an enumeration of dates of the form yyyy-mm-dd

3. Journal editorial activity -- from an enumeration of journals by issn

4. Person holding editorial activity -- from an enumeration of people by label

5. Editorial Role -- either "editor" \(for all kinds of editorships\) or "reviewer" for all kinds of reviewers.

6. Editorial Role label -- open text -- further describes the role as needed.  Examples: "Editor in Chief" or "Applications Reviewer"

Simple VIVO will work with whatever data you have -- any of the attributes can be left blank.  But an editorial activity without a journal or person or role is not expected by the users of VIVO.

## The steps to manage editorial activities

1. Update your enumerations using \`python make\_enum.py\`

2. Get editorial activities from your VIVO using \`python sv.py -a get\`

3. Edit your spreadsheet \`editorial.txt\` correcting and adding information for existing editorial activities, and adding new editorial activities, one row per editorial activities.  If a person has five editorial activities, use five rows for that person. Use a text editor or spreadsheet program to edit \`editorial.txt\`

4. Update the editorial activity information in your VIVO using \`python sv.py -a update\`

Repeat the steps as necessary.

