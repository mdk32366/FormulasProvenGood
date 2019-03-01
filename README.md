### FormulasProvenGood
Formulas that are known working formulas - Especially for DATES

Calculating business days between date fields:

( (5 * ( FLOOR( ( DATEVALUE([Project__c].LastModifiedDate) - DATE( 1900, 1, 8) ) / 7 ) ) + MIN( 5, MOD( DATEVALUE([Project__c].LastModifiedDate)- DATE( 1900, 1, 8), 7 ) ) )
-
(5 * ( FLOOR( ( DATEVALUE( [Project__c].CreatedDate) - DATE( 1900, 1, 8) ) / 7 ) ) + MIN( 5, MOD(DATEVALUE([Project__c].CreatedDate) - DATE( 1900, 1, 8), 7 ) ) ) ) >= 10

Note the use of DATEVALUE.
