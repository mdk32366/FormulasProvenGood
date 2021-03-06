### FormulasProvenGood
Formulas that are known working formulas - Especially for DATES



## Formula for working with DATETIME types (System dates especially) in Salesforce (5/9/2019)

1.  In Process Builder, for your task or deliverable, or whatever, make a Due Date Only field, make it a formula field, then you can add days in terms of additional seconds with the following.

Created Date Field (Insert Correct Field Name) + (24*number of days)*60/1440

To add 28 days, use the following:  (24*28)*60/1440.


## Calculating business days between date fields:

( (5 * ( FLOOR( ( DATEVALUE([Project__c].LastModifiedDate) - DATE( 1900, 1, 8) ) / 7 ) ) + MIN( 5, MOD( DATEVALUE([Project__c].LastModifiedDate)- DATE( 1900, 1, 8), 7 ) ) )
-
(5 * ( FLOOR( ( DATEVALUE( [Project__c].CreatedDate) - DATE( 1900, 1, 8) ) / 7 ) ) + MIN( 5, MOD(DATEVALUE([Project__c].CreatedDate) - DATE( 1900, 1, 8), 7 ) ) ) ) >= 10

Note the use of DATEVALUE.


## Days Until a Date

([Company_Certification__c].Expires__c ) <= Today() + 30


## Formula for comparing previous periods to subsequent or present periods (subscriber attrition in paying customers)

To compare a value to the highest value in a previous grouping, use a formula like this:

IF(MAX(
BLANKVALUE(RowCount,0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 1),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 2),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 3),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 4),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 5),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 6),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 7),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 8),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 9),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 10),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 11),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 12),0)
) > 0, 
RowCount / MAX(
BLANKVALUE(RowCount,0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 1),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 2),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 3),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 4),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 5),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 6),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 7),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 8),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 9),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 10),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 11),0),
BLANKVALUE(PREVGROUPVAL(RowCount, CLOSE_DATE , 12),0)
),
/*ELSE*/
0
)


Then to compare a value to its immediate predecessor, use this:

IF(PREVGROUPVAL(RowCount, CLOSE_DATE) > 0,
RowCount / PREVGROUPVAL(RowCount, CLOSE_DATE),
/*ELSE*/
0
)

Be sure to set the formatting to display at your Row Grouping and Column Grouping intersection of data.


