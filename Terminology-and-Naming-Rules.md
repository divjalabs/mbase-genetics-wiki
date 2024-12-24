# Terminology
- **Reference table of alleles/ Allele reference table** - table that lists and defines the different alleles associated with specific genetic markers.
- **Table of genotypes** - table that records the genetic makeup of individual samples at specific genetic markers.
- **Organization** - group of users.
- **Allele names mapping table** - a table used to associate user-defined allele names with the database-stored allele names.

# Naming Rules
## Samples
Names of samples in the database follow a strict naming rules since the the database is setup in a way that the sample code is also the sample database entry unique identifier.

Naming of the samples must follow the following rules:

- Exactly 6 characters.
- All **letters** are **uppercase**.
- First three [1-3] characters are all **letters from A-Z**.
- Second three [4-6] characters are must be selected from: `012345678ACEFHJKLMPTUX`.
- regex notation `^[A-Z]{3}[012345678ACEFHJKLMPTUX]{3}$`.

## Individuals
The names of individuals on the database level should be unique.  
Database maintainers propose an naming convention that the individual is named by the sample code of the sample with the best genotype at the time when a particular individual was firs detected.

## Markers
The same markers must have identical names in all the import data tables!
Current naming convention for naming markers:
 - Marker name consist of a prefix and a number.
 - No whitespace characters anywhere in the name.
 - First letter of the prefix is capitalized, and the remaining letters are lowercase

## Alleles
When importing the data (in the Reference table of alleles) the naming of alleles can fallow any user defined allele naming scheme since the database performs automatic allele renaming during the import of data.

However the database stores the alleles by predefined rules:
 - Names of alleles are based on the length and sequence variation.
 - Names of alleles must be unique on per-marker basis.
 - Name of the allele is the length of the sequence
 - Variants of alleles with the same length but different nucleotide sequence are distinguished by `_` followed by the variant number. (eg. on the same marker there are three alleles with the length of the sequence equal to 54, in the database they are distinguished as `54`, `54_1`, `54_2`)
 - The variant number is assigned based on the time of import of that allele (the first allele gets named just by its length, if there is a second allele of the same length present it receives the variant number `_1`, the third allele variant with the same length receives the variant number `_2` and so on.)


|Allele|Marker|Sequence|
|:----:|:----:|:----:|
|9     |Marker1|accaccacc|
|9_1   |Marker1|acc**acg**acc|
|9     |**Marker2**|accaccacc|
## Genotypes
When importing the data (Table of genotypes) the genotype names must consist of the allele names listed in the Reference table of alleles. The genotype of an individual on a particular marker is represented by allele names separated by whitespace character.

When preparing the Table of genotypes for import the user must follow 2 rules:
  1. The allele names in the Reference table of alleles and in Table of genotypes must be the same
  2. Genotype is represented by two allele names separated by whitespace.

As with storing allele data, the same applies to genotype data: when genotypes are stored in the database, they are renamed according to the naming conventions listed in the alleles section.

## Date format
Although the database accepts various date notation formats it outputs the date or datetime values as `YYYY-MM-DD` or `YYYY-MM-DD HH:MM:SS.SSSS`. 
