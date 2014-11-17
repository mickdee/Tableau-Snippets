Tableau Snippets
================

Cheatsheet for a variety of formatting, calculating, and dashboarding needs

## FILTERING

#### Picking specific items to appear in quick filter
Create a "set" by R-clicking on anything in the filter shelf and selecting only the elements you want to appear in the filter

#### Use a calculation to filter a specific field
Example:  
```
IF [Dimension] = "Value"
THEN [Measure]
END  
```  
This is useful when you want a filter to apply to only a single field on a worksheet

## PRO TIPS

When in doubt, right-click on stuff. Almost everything in Tableau has parameters or sub-menus that can be set to customize formatting or other options in your view.

#### Greens vs Blues = Continuous vs Discrete 

There is surprisingly little documentation in the interface (if any) that tells you the magic of simply understanding the difference between green and blue things. 

Green = Continuous (create axes). But what does that mean? Think of continuous like a spectrum with no beginning or ending point. A date field set to continuous will have an axis that can be oriented to any position along the spectrum of time -- allowing you to customize the view as tightly or broadly around a range of dates as you like. 

Blue = Discrete (create headers). Discrete data assumes the max and min values in your dataset are absolute endpoints. There is nothing higher or lower that can be viewed. The axis of a date field set to discreet will not appear as an endless spectrum then, but as unique intervals that can be filtered or analyzed independently.

This distinction exists so that you can use continuous dimensions or discrete measures in the view.

Aggregate calculations are always measures.

## NUISANCES

#### Remove 'ABC' placeholder in lists
1. Remove "Show Header" check box
2. Drag another instance from data window onto "Text" mark shelf  
OR  
1. Create a calculated field " " and place on marks shelf

## USING CALCULATED FIELDS

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

## MAKING MAPS

#### Projections
Tableau default projection is WGS 84

#### Reverse Geocoding
+ Have a dataset with a bunch of lat / long coordinates and want to make filled maps or other views that aggregate the data by city, state, or country? Well, sadly, Tableau doesn't offer any way to do this process (often called "reverse geocoding") out of the box.
+ Do not dispair, however, as there are plenty of free tools on the Web that will process lat/longs and spit out street addresses. These tools are great for small datasets, but don't plan on much success with thousands of records -- at least not quickly.

## CLEANING DATA

#### Corrcting date records that only contain year 
Create a calculated field to add day and month to year values:
DATE("01-01-"+[FY_Year])  
OR  
DATE("01/01/" + STR([Year]))

#### Removing Units (ex: sq ft) from numbers and converting to usable measures
```
FLOAT(
    REPLACE(
        (LEFT([Dimension], FIND([Dimension]," "))) , ",", "" 
        )
)
```

## BUILDING DASHBOARDS

#### URL Actions
Use Case: when I click a field I want the wikipedia page for that field to appear
Note: URL must be included in your dataset for each record

1. Add wikipedia URL to level of detail shelf on the corresponding view
2. Create an action that uses the sheet with the field you want to click as the source 
3. Instead of having a target sheet, add the wikipedia URL field which will now be available as an option, because it has been added to the level of detail shelf on the corresponding worksheet

#### Navigate between Dashboards
1. Create calculated field with the text of your link, ie "Click Here to go to Dashboard 2"
2. Add new calculated field to a sheet
3. Add sheet to your source dashboard and create an action that points to the target dashboard

## CUSTOMIZING VIEWS

#### Custom Shape Marks
1. In order for Tableau to recognize custom images for shapes they must be saved in the repository which is typically found in your Documents folder here: Documents -> My Tableau Repository -> Shapes.  
2. In the shapes directory you'll find all the shape sets which Tableau uses automatically.
3. Create a new directory here and throw in your new shape images. Shape images should ideally be square and sized no bigger than 32 X 32 

#### Forecasting
+ Forecasting is finnicky and only works well if the view has LOTS of data points and the criteria below are satisfied:
+ No table calculations can be applied to the current view
+ Also check to make sure your view has no totals or percentages displayed on the view (not supported)
+ Time series should be set to regular intervals (at least 5) without null values
+ No measures can be on the filter shelf
+ Only one aggregate measure is allowed per pane. Also remove "Measure Names" and "Measure Values" fields.

#### Table Options
+ By default, Tableau will only allow tables with 6 levels of row labels (fields).
+ To adjust this, Navigate to Analysis > Table Layout > Advanced
+ In the "Table Options" dialog that appears, you can adjust the max number of levels allowed up to 16 for rows and columns

## ADDING THE FINISHING TOUCHES

#### Dynamic tooltips
+ In a tooltip, you can place summary statistics as well as and dimension / measure used in the view or placed on the marks shelf
+ Example: <Dimension> is landed on <AGG(Measure (pct))> of the time.

#### Hide specific mark labels
R-Click on label and select "Never Show"

#### Showing Data Refresh Date on a View
Showing data refreshed date can be added to the title of any worksheet, but not standalone text boxes on dashboards

1. Edit the title of your worksheet by selecting the carat at the top right corner of the title and choosing "Edit" 
2. select the "Insert" dropdown and add "Data Update Time" 

#### Adding symbols to tables and tooltips
1. Examples symbols in tables: to insert downward facing triangles for negative values, click the measure pill and select Format
2. In the Numbers drop-down box, select Custom, then copy and paste the down icon in the Format box.
+ You can also add icons to tooltips by creating separate calculated fields for the positive and negative icons - tutorial here: https://www.broadbandmetrics.com/display/Public/2014/04/28/Tableau+Pro+Tip%3A+Adding+Icons+to+Tables+and+Tooltips

## SHARING WITH TABLEAU PUBLIC

#### Publish multiple views from the same workbook
1. In your workbook, hide all tabs / views you don't want people to be able to navigate to
2. Save to Tableau Public
3. Go to your published workbook settings (on the Tableau Public site), check "show sheets as tabs"

## HOTKEYS
+ Swap Axes: Ctrl + w
+ Presentation Mode: F7
+ Clear Worksheet: Ctrl + Alt + Backspace
+ New Worksheet: Ctrl + M
+ Connect to Data: Ctrl + D
+ Refresh source data (not extract): F5