Tableau Snippets
================

Tableau tidbits for a variety of formatting, calculating, and dashboarding uses

## Filtering

#### Picking specific items to appear in quick filter
Create a "set" by R-clicking on anything in the filter shelf and selecting only the elements you want to appear in the filter

#### Use a calculation to filter a specific field
Example:  
```
IF [Dimension] = "Value"
THEN [Measure]
END  
```  
This is useful when you don't want a filter to apply to only a single field on a worksheet

## Nuisances

#### Remove 'ABC' placeholder in lists
1. Remove "Show Header" check box
2. Drag another instance from data window onto "Text" mark shelf  
OR  
1. Create a calculated field " " and place on marks shelf

## Calculated Fields

#### Basic IF Statement

```
IF sum([Measure]) > [Parameter] THEN "Too Large"
ELSE "Just Fine"
END
```

#### ELSEIF Statement
```
IF SUM([Measure]) >= [Paremeter] THEN "High"
ELSEIF SUM([Measure]) >= [Parameter] AND SUM([Measure]) <= [Parameter] THEN "Medium"
ELSE "Low"
END
```

#### Operators allowed in Calculations
```
= = or = (Equal to)
!= or <> (Not equal to)
>
<
>=
<=
AND / OR logical operators
```

#### Count Distinct
1. create this calculated field: ```SIZE()```
2. Then drop it onto the worksheet and have it compute along whatever dimension you want a distinct count of. SIZE() counts the number of rows in a partition.

## Mapping

#### Projections
Tableau default projection is WGS 84

## Data Cleaning

#### Corrcting date records that only contain year 
Create a calculated field to add day and month to year values:
DATE("01-01-"+[FY_Year])  
OR  
DATE("01/01/" + STR([Year]))

## Finishing Touches

#### Dynamic tooltips
+ In a tooltip, you can place summary statistics as well as and dimension / measure used in the view or placed on the marks shelf
+ Example: <Dimension> is landed on <AGG(Measure (pct))> of the time.

#### Hide specific mark labels
R-Click on label and select "Never Show"

#### Showing Data Refresh Date on a View
Showing data refreshed date can be added to the title of any worksheet, but not standalone text boxes on dashboards``
1. Edit the title of your worksheet by selecting the carat at the top right corner of the title and choosing "Edit" 
2. select the "Insert" dropdown and add "Data Update Time" 

## Dashboards

#### URL Actions
Use Case: when I click a field I want the wikipedia page for that field to appear``  
1. Add wikipedia URL to level of detail shelf on the corresponding view
2. Create an action that uses the sheet with the field you want to click as the source 
3. Instead of having a target sheet, add the wikipedia URL field which will now be available as an option, because it has been added to the level of detail shelf on the corresponding worksheet

#### Navigate between Dashboards
1. Create calculated field with the text of your link, ie "Click Here"
2. Add new calculated field to a sheet
3. Add sheet to your source dashboard and create an action that points to the target dashboard

#### Custom Shape Marks
1. In order for Tableau to recognize custom images for shapes they must be saved in the repository which is typically found in your Documents folder here: Documents -> My Tableau Repository -> Shapes.  
2. In the shapes directory you'll find all the shape sets which Tableau uses automatically.
3. Create a new directory here and throw in your new shape images. Shape images should ideally be square and sized no bigger than 32 X 32 

## Tableau Public

#### Public multiple views from the same workbook
1. In your workbook, hide all tabs / views you don't want people to be able to navigate to
2. Save to Tableau Public
3. Go to your published workbook settings (on the Tableau Public site), check "show sheets as tabs"