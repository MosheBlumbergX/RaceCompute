# RaceCompute

Step by step on how to make easy race results entries and compute.   

[Example in google sheet ](https://docs.google.com/spreadsheets/d/1NWXwv5VSuLRH6ptMHkPPIhTXmVkEqkVxTKUloUXtz4E)

## Full export from entrant site  

Example: [ExportFromRaceSite](https://docs.google.com/spreadsheets/d/1NWXwv5VSuLRH6ptMHkPPIhTXmVkEqkVxTKUloUXtz4E/edit#gid=279737281) sheet.   
A normal export from an entry site will have the following columns:  
```
Event
Event Date
RaceNumber
Gender
FirstName
Surname
AgeOnDay
DoB
Club
Team
Type
Address
Address1
Address2
Address3
PostCode
Phone
Email
Medical Conditions
EntryDate
EntryPaid
EntryID
EntrantID
AffRef
EntryCost
Fee
Q1
Q2
Q3
Q4
Q5
Q6
OpEx1
OpEx2
OpEx3
OpEx4
OpEx5
Donation
ShowOnEntrantList
DataProtect
Trans-Date
Trans-FirstName
Trans-Surname
Trans-Club
Trans-Gender
Trans-DoB
Trans-Email
TQ1A
TQ2A
TQ3A
TQ4A
TQ5A
VoucherValue
VoucherCode
VoucherTitle
```


## Taking what you need

### Raw sheet 

Example: [Raw](https://docs.google.com/spreadsheets/d/1NWXwv5VSuLRH6ptMHkPPIhTXmVkEqkVxTKUloUXtz4E/edit#gid=681996296) sheet.

You need only the followings for the RAW sheet:  
```
RaceNumber
Gender
FirstName
Surname
AgeOnDay
Club
Team
CATALL
cat groups
Categories
CAT AGE
CAT-G|F
```  

#### Compute 1:  
Takes the age on day column and fit it into the right category of age
```
=ArrayFormula(vlookup(E2:E86,I2:I8,1))
```  
#### Compute 2: 
Takes the age group and the gender column and connects it.  
```
=(B2&K2)
```  
#### Compute 3:  
Takes the new `<gender><ageGroup>` and filter out the senior portion. 



### RaceNumberPositionResult

Example: [RaceNumberPositionResult](https://docs.google.com/spreadsheets/d/1NWXwv5VSuLRH6ptMHkPPIhTXmVkEqkVxTKUloUXtz4E/edit#gid=1672809147) sheet.  

A table with 3 columns:  
```
RACE NO	
POSITION
RESULT
```

You will start with empty `POSITION` and `RESULT`.  
As the finisher comes in you will log their result based on the `RACE NO`.  

When all are entered (or majority as this can be added later), sort by `RESULT` and populate the `POSITION` column with consecutive numbers (1,2,3), for example:  
| RACE NO |      POSITION     |  RESULT  |
|:-------:|:-----------------:|:--------:|
|   138   |                 1 |  0:27:10 |
|    10   |                 2 |  0:29:16 |
|   140   |                 3 |  0:29:21 |
|    59   |                 4 |  0:29:47 |
|   112   |                 5 |  0:30:09 |
|   101   |                 6 |  0:31:01 |


#### Auto fill numbers

* Type a value in the next cell to establish a pattern.
  * Tip: For example, if you want the series 1, 2, 3, 4, 5..., type 1 and 2 in the first two cells. If you want the series 2, 4, 6, 8..., type 2 and 4.
* Select the cells that contain the starting values.
* Drag the fill handle across the range that you want to fill.


### Results-Full-From-Entry-System

Example: [Results-Full-From-Entry-System](https://docs.google.com/spreadsheets/d/1NWXwv5VSuLRH6ptMHkPPIhTXmVkEqkVxTKUloUXtz4E/edit#gid=1703698175) sheet.

```
FirstName
Surname
Club
Team
RaceNumber
CATEGORY
POSITION
RESULT
Local Winner
```

#### Compute 1:  

Check to position based on time and race number logged in the [RaceNumberPositionResult](https://docs.google.com/spreadsheets/d/1NWXwv5VSuLRH6ptMHkPPIhTXmVkEqkVxTKUloUXtz4E/edit#gid=1672809147) sheet.  
```
=VLOOKUP(G2,RaceNumberPositionResult!A:C,2,False)
```

#### Compute 2:  

Check to result based on time and race number logged in the [RaceNumberPositionResult](https://docs.google.com/spreadsheets/d/1NWXwv5VSuLRH6ptMHkPPIhTXmVkEqkVxTKUloUXtz4E/edit#gid=1672809147) sheet.  

```
=VLOOKUP(G2,RaceNumberPositionResult!A:C,3,False)
```