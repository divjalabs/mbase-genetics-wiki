Filtering samples and genotypes is done trough the main window of genetic samples browser. Available filters are visible on the right side of the general actions ribbon on top of the browser.![image](uploads/fe664347424e66026840a6afa47ee974/image.png).

Three filter buttons are avalible for users:
  1. All filters
  2. Shared
  3. Individuals

## All filters

The **All filters** button ![image](uploads/38a309e5014e534c7f13907af8fecd0b/image.png) allow the user to filter the samples based on any available [sample metadata attribute](Importing-sample-metadata/{Sample-metadata-attributes})

When selecting the **All filters** a new filtering window opens where the user can specify the filter options:
 - Field
 - Condition
 - Value (appears after selecting the Field option)
 
![image](uploads/46a040d40c50286bb63961e5df84d7af/image.png)

### Field
The field option holds a list of all avalible attrubutes on which the filtering process can be applied

### Condition
The condition option allow the user to select the the filtering operation

| Operator | Description             | Remarks |
|----------|-------------------------|---------|
| `<`      | Field less than Value   |only fields with **numeric** values (eg. `Sample age`)|
| `>`      | Field more than Value   |only fields with **numeric** values (eg. `Sample age`)|
| `=`      | Field equal to Value    |all fields        |
| `<>`     | Field not equal to Value| only fields with **numeric** values (eg. `Sample age`)          |
| `LIKE`   | Field matches Value pattern (e.g., with wildcards `%`)|only field with **string** values         |


### Value
Under the value option the user need to specify the desired search term for the filter clause. For attributes that have a code list in the database (e.g., sample type), the user can select the search term form a dropdown menu of the code list options.

### Multiple Filter Clauses  

The filtering procedure allows users to apply multiple filter clauses. To filter data that satisfies multiple clauses, the user adds additional filter conditions to the filter table and then selects the logical operator to define the relationship between the clauses. The database supports two logical operators: `AND` and `OR`.  


### >*Example: One filter clause*

>Filtering all scat samples from the database

Filter clause for achieving this would be `Sample type = scat`.
Procedure:
  -  under **Field** select `Sample type`.
  -  under **Condition** select `=`.
  -  under **Value** select/type in `scat`.


![image](uploads/c0d854fc6597aa8deab8ca341e111f1f/image.png)

when the filter clause fields are all filled with desired value the user must select **Add** ![image](uploads/ac61a39e5f9ecf7e4ce371f8d9477368/image.png), so that the filter clause gets written in the filter table.
![image](uploads/9010e3386e16ddbcc1d11d77d2e450ff/image.png)

To get the filtered data the user must click on the apply button ![image](uploads/3916f2119907fc342c77eddb816aaadc/image.png).


### >*Example: Multiple filter clauses*

> Filtering all scat samples collected after 2024-01-01 from the database.

The two filter clauses needed for getting this data would be
  - `Sample type` `=` `scat` 
  - `Date (YYY-MM-DD)` `>` `2023-12-31`

The logical operator in this case would be `AND` since both conditions have to be meet to get the desired samples. The logical operator can be set in the **Operator** column of filter table.

![image](uploads/737f7fa1bee1b1417bd0ca5f1de450ab/image.png)

> Filtering all scat or urine samples

The two filter clauses needed for getting this data would be
  -  `Sample type` `=` `scat` 
  -  `Sample type` `=` `urine` 

The logical operator in this case would be `OR` since ether of conditions have to be meet to get the desired samples. The logical operator can be set in the **Operator** column of filter table, to change it for `AND` to `OR` the user needs to click on the blue text (AND/OR) inside the cell of the **Operator** column.

![image](uploads/cfcf6bdff684d91f68a871c3341155fa/image.png)

## Shared
The **Shared** button ![image](uploads/eabe1a051b2d5ddcd0e5fbbec277beda/image.png) enables users to filter samples based on their [accessibility to the user](Genetic samples-user-access-control).
There are three option that user can choose by clicking on the slider icon ![image](uploads/918651c458ca3dd487c255f96ef2f6f7/image.png):

1. Shared with me  
*This option shows the data of other users shared with me or with organisations       I am a member of.*
2. Shared by me  
*This option shows the data uploaded by me and shared with other organisations or/and users.*
3. Uploaded by other  
*This option shows the data uploaded by others and not shared with you - you can manage this data because you are a module administrator.*

![image](uploads/e5954db436bfb26f403464a59c8776b0/image.png)

## Individuals

The **Individuals** button ![image](uploads/bee8ecf2f3652a8dca9f6132741cb351/image.png) serves as a shortcut for filtering samples by the individuals they are associated with.
