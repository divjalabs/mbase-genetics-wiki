---
Importing genotypes - input file format and data validation
---









## Basic rationale
![basicrationale.drawio.svg](uploads/3b521ccdc6ab5d1786f353d39516290c/basicrationale.drawio.svg)


## Import data structure

Genotypes are imported from the **Excel** `.xlsx` file which is to have at least **two pages**:
  1. reference table of `alleles` 
  2. table of `genotypes`

> **IMPORTANT NOTE:**
All of the alleles present in the (2) genotype table have to be referenced in the (1) reference table of alleles. 

[example dataset - 5 samples](uploads/40ad96341eb849cfe890953710470bb2/small_example.xlsx)

### Reference table of alleles

**TABLE COLUMNS**

The table has to have at least 3 columns:
 - Allele: name of given allele
 - Marker: name of marker
 - Sequence: sequence of nucleotides present at this allele

**TABLE FORMATTING**

 - The **mandatory columns** must always be ordered in this sequence: (1)*Allele*, (2)*Marker* and (3)*Sequence*. 
 - The **first row** must hold column names. 
 - **Column names** are adaptable, with no strict adherence to predefined naming conventions
 - For rules about the table content see [Terminology and Naming Rules](Terminology-and-Naming-Rules) chapter.

**EXAMPLE**

| Allele   | Marker | Sequence                                                                              |
|:----:|:------:|------------------------------------------------------------------------------------------|
| 44   | Cl147  | ttcaatagatagatagatagatagatagatagatagatagatag                                             |
| 68   | Cl147  | ttcaatagatagaaatgatagatgatagatagatagatagatagatagatagatagatagatagatag                     |
| 55   | Cl233  | aaaaagaaagaaagaaagaaagaaagaaagaaagaaagaaagaaagaaagaaagt                                   |
| 59   | Cl233  | aaaaagaaagaaagaaagaaagaaagaaagaaagaaagaaagaaagaaagaaagaaagt                               |
| 57   | Cl264  | atagatagatagatagatagatagatagatagatagatagatgatagcatttattat                                 |
| 61   | Cl264  | atagatagatagatagatagatagatagatagatagatagatagatgatagcatttattat                             |
| 61_2 | Cl264  | gcagatagatagatagatagatagatagatagatagatagatagatgatagcatttattat                             |

### Table of genotypes

Given as animal ID x marker matrix.
|            | *marker 1 (m<sub>1</sub>)* | *marker 2 (m<sub>2</sub>)* | ... | *marker n (m<sub>n</sub>)* |
|------------:|:--------------------------:|:--------------------------:|:---:|:--------------------------:|
| *sample 1 (s<sub>1</sub>)* | genotype <br> m<sub>1</sub>s<sub>1</sub> | genotype <br> m<sub>2</sub>s<sub>1</sub> | ... | genotype <br> m<sub>n</sub>s<sub>1</sub> |
| *sample 2 (s<sub>2</sub>)* | genotype <br> m<sub>1</sub>s<sub>2</sub> | genotype <br> m<sub>2</sub>s<sub>2</sub> | ... | genotype <br> m<sub>n</sub>s<sub>2</sub> |
| ...                | ...                          | ...                          | ... | ...                          |
| *sample n (s<sub>n</sub>)* | genotype <br> m<sub>1</sub>s<sub>n</sub> | genotype <br> m<sub>2</sub>s<sub>n</sub> | ... | genotype <br> m<sub>n</sub>s<sub>n</sub> |


**TABLE FORMATING**

 - **First column** must give the information about sample code. 
 - **All subesquent columns** hold the information about the genotype of particular sample on particular marker.
 - The order of **marker columns** is not important.
 - **First row** must hold column names, which in this case represent **marker names**.
 - For rules about the table content see [Terminology and Naming Rules](Terminology-and-Naming-Rules) chapter.


**EXAMPLE**

| Sample | Cl147  | Cl233  | Cl264   | Cl274  | ... | Lup23 | ZFX | ZFY |
|:------:|:------:|:------:|:------:|:------:|:------:|:------:|:------:|:------:|
| PTYTII |        |        |         | 57 57  | ... |       | 83 83   | 69 69   |
| WTZMBY | 44 73  | 59 71  | 57 61   | 61 61  | ... | 55 55 | 83 83   | 69 83   |
| OWXVEN | 44 69  | 55 67  | 61 61   | 57 57  | ... | 55 59 | 83 83   | 83 83   |
| MPTOXZ | 68 68  | 55 59  | 61_2 69 | 61 61  | ... | 55 55 | 83 83   | 69 83   |
| AEGBXJ | 68 68  | 55 59  | 61_2 69 | 57 61  | ... | 55 59 | 83 83   | 83 83   |

## Data validation
1. Allele reference table data is filtered for the missing allele name, marker or sequence as this data are necessary for the genotype import.

2. The genotype page is validated with the filtered reference table data (rows with missing allele name, marker or sequence field removed) against the following criteria:
   - empty sample code
   - sample code in wrong format
   - missing allele pair
   - unreferenced allele name
   - multiplicated sample row

> **IMPORTANT NOTE**: All the rows in the allele reference table data which are not referenced from the genotypes table are discarded.

3. The referenced alleles from the allele reference table are checked for the:
 - repeated sequence with different allele name
 - repeated allele name with different sequence

---

If all the conditions from the step 2 and 3 are satisfied then:
- the duplicates are removed from the referenced alleles in the allele reference table
- the genotypes are imported into the database following the database allele naming schema
- the user is presented with the "Import successful" page and possibility to download the mapping between the imported allele names and the allele names defined by the database. Additionally, the import report consists of number of newly added samples with genotype and number of existing samples where the genotype was added. 

## Allele reference table
- 1st line is assumed to be header and is ignored in the import, the columns are to be in the following order:
   - allele name
   - marker
   - nucleotid sequence 

> **IMPORTANT NOTE:** If any of the upper field values is missing in the row, then the row is discarded from the import. All the discarded rows are listed in the import report.

After the import allele sequence reference table is imported and filtered for the missing field values and duplicated rows two conditions are validated:

1. the same sequence on the same marker is to have the same name
2. different sequence on the same marker is not to have the same name

[image](uploads/80c6cc1c1579fbe3e6de42cf4493ca0f/image.png)

|allele|marker|sequence|does not conform <br> to condition 1|does not conform <br> to condition 1|
|:----:|:----:|:----:|:----:|:----:|
|5|LUP2|AAGAA|**X**||
|5_2|LUP2|AAGAA|**X**|**X**|
|5_2|LUP2|GAAGA||**X**|
|5|Cl274|AAGAA|||

According to the user's preference (as selected in the import dialog), the offending rows are either imported following the database naming schema or discarded from the import process.

Only uniquely identifiable combinations will be imported.

For every imported sequence-marker pair, the originally imported names can be downloaded.

## Samples' genotypes table
- in the first column of this table sample codes are expected. 
- the first row must containt marker names. The first field (A1:1) is ignored as it is the header of sample codes column.

There are two options regarding sample codes when importing the data:

- sample codes follow the coding system in the database
- sample codes use a custom coding system

### Sample codes follow the coding system in the database

- if a sample with the same code exists in the database but lacks genotype information, the genotype from the uploaded sample will be added to it.
- if a sample with the same code exists in the database and already has genotype information, the genotype from the uploaded sample will not be imported.
- if a sample with the specific code does not exist in the database, it will be added along with the genotype information from the uploaded sample.

---

**The coding system for the database requires:**
- Exactly 6 characters.
- All **letters** are **uppercase**.
- First three [1-3] characters are all **letters from A-Z**.
- Second three [4-6] characters are must be selected from: `012345678ACEFHJKLMPTUX`.
- regex notation `^[A-Z]{3}[012345678ACEFHJKLMPTUX]{3}$`.

### Sample codes use a custom coding system

All the samples with a valid genotypes are going to be imported. Random database sample code will be generated and your sample code will be stored in the 2nd lab code field.[small_example.xlsx]