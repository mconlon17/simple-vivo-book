# Data  Management

Data management a collection of processes and permissions and talents applied. To the task of creating quality data.  Quality data is data is data that is correct and of value to consumers of the data.  

## Focusing effort on high value data

VIVO represents the scholarship of your organization.  It can represent a very broad collection of various kinds of activities of scholars -- the production of scholarly works, the acquisition of research funding, the teaching and mentoring of trainees,  service to the profession, as well as details about the training and background of each person participating in the scholarship of the organization.  Simple VIVO, as described in this book, focuses the collection and management of data on attributes of scholars that have high value for organizations.  This focus enables us to manage data with a reasonable amount of effort.  

Other choices could be made.  simple VIVO is extensible.  It can be used to manage any VIVO data, and actually, any semantic data.  The data need not be the data described in the examples provided with Simple VIVO.  See Extending Simple VIVO and the Pump descriptions of the definition file to see how Simple VIVO. can be extended to manage additional or different attributes regarding scholarship or other domains.

## Authoritative Sources of Data

For every value in VIVO we should be trying to answer the question "who is the best source of this data?"  For different examples, the answers are likely to be different.  See the table below for possible answers.  The answers for your organization may be different.

Example | Best source
------|------
Employee information | Human resources
Teaching | The Registrar
Grants | Office of Research
Research areas | Individual faculty members
Publications | Publishers and indexers
Books | individual faculty members
Educational Background | The Provosts office
Clinical activities | Health center
Extension activities | extension office
Service to the profession | individual faculty
Mentoring | graduate School

May offices of your university may be best sources of information for VIVO.  Perhaps their information has already been extracted and made available through a data warehouse.  You may be able to use the data warehouse to provide data for your VIVO.  In other cases, the data may need to come from the office to you.  This may be able to done done in the form of a spreadsheet that can serve as input to you Simple VIVO processes.

Notice that some of the "best sources" are the faculty themselves.  How I'll you collect this information from the faculty?  Will faculty edit their information in VIVO?  How will you follow up with faculty that do not provide information?

For each of the examples provided with Simple VIVO, we will assume that you have the data you need.  We understand that. Getting the data from the various authoritative sources may require effort.

## Values -- correct, missing, and incorrect

In Simple VIVO, whatever value you provide in the spreadsheet will replace the value in VIVO.  Simple VIVO always assumes that the value in the spreadsheet is correct, or preferred, or better than the value in VIVO.  When the value in the spreadsheet is the same as the value in VIVO, no work is done, the value in VIVO remains unchanged.  When VIVO does not have a value, the value in the spreadsheet is added to VIVO.

In some cases, we may learn that the value in VIVO should be removed and should not be replaced with another value.  VIVO may have a value that is incorrect, or it may have. A value that for some reason, should not be present in VIVO.  Simple VIVO provides a special value "None" that is used in Simple VIVO to indicate that the value in VIVO should be removed and should not be replaced with another value.  data managers sometimes. Refer to such values (or actually the lack of a value) as a missing value.  To indicate a missing value, use the special value "None". If VIVO does not have a value, and the value. In the spreadsheet is None, no work is done and VIVO remains without a value.  If VIVO has a value, and the value in the spreadsheet is None, the value in VIVO is removed.

In some cases, data you receive from authoritative sources may be incorrect.  You will need to decide how to address such cases if they should arise.  For example, you may receive data regarding the phone numbers of the faculty only to find that phone numbers do not contain the required number of digits, or have other validity problems.  You may know of "better" phone numbers for one or more faculty.  VIVO data managers often discover such concerns.  It is customary to report the problems to the data provider.

In addition to providing values which replace values in VIVO, and providing the special value None to indicate that a value in VIVO should be removed, simple VIVO has a third important way of indicating what should be done as spreadsheet values are considered for inclusion in VIVO.  A spreadsheet value can be blank or empty.  When spreadsheet values are blank or empty, Simple VIVO interprets this as "do nothing".  All blank and empty spreadsheet values are ignored during processing.

## Binary values

Some values in Simple VIVO are defined as being binary -- that is, the value represented by the column is either present or absent in VIVO.  Use a "1" in a binary column to indicate the presence of the value.  Use "0" to indicate the absence of the value.  "None" continues. To indicate that no value should be recorded.  And blank continues to mean that no action should be taken.

## Sets of Values

When managing data in VIVO, we need to. Be clear whether an attribute can have one value, or more than one value.  VIVO often supports more than one value, but Simple VIVO may simplify the data management to the case of one value. For each example, we indicate the values that can be managed and whether the value is single, multiple, or binary (present or absent).

When Simple VIVO accepts multiple values for a value, put all the values in a single spreadsheet cell, separated by the "infra field delimiter" st in the sv.cfg file and defaulted to a semicolon.

As always, the values you specify in the spreadsheet will replace the values in VIVO.  If you use the word None in a multi-valued field, all the values in VIVO will be removed.  Leaving a multi-valued field blank indicates that no action should be taken on the field.

# Summary

You will need to identify sources for each of the domains you choose to manage in Simple VIVO' as well as procedures for acquiring the data, getting the data. Into the format required by Simple VIVO, and handling cases where the authoritative data may be incorrect.

Simple VIVO spreadsheet cells can contain any of the following

Value | meaning
-----|-----
A single value | Replace the value in VIVO with the value in the spreadsheet
None | remove the value in VIVO and do not replace it
Blank | do nothing
Multiple values separated by semi-colons |  Replace the values in a multi-valued set with the values. In the spreadsheet
0| for a binary column, remove the value represented by the column
1| for a binary column, add the value represented by the column











