# Value Constraints (including some NOT NULL constraints)

## Global

* Text fields should not have leading or trailing white spaces. (Are there any fields for which this is not the case?)  <font color='red'>
This can be checked with
      ```
      CHECK(TRIM(FROM <columnname>) = <columnname>)
      ```
Probably sequences of two or more consecutive whitespace characters should be forbidden as well except for various free-form textual columns such as `traits.notes`.  This can be checked with
      ```
      CHECK(REGEXP_REPLACE(TRIM(FROM <columnname>), ' +', ' ') = <columnname>)
      ```
For convenience, we should probably define a function so we can just do something like
      ```
      CHECK(is_normalized(<columnname>))
      ```
.</font>

## covariates:

*	Check that `level` is in the range corresponding to variable referenced by `variable_id`.
*	Check that `n` is positive <font color='red'>(or > 1 ?)</font> if it is not NULL.
*	<font color='red'>Check that `statname` and `stat` are either both NULL or both non-NULL.  (Alternatively, ensure that `statname` is non-NULL and that it equals the empty string if and only if `stat` is NULL.)
*	Check that `statname` is one of "SD", "SE", "MSE", "95%CI", "LSD", "MSD" or possibly "".  Consider creating an ENUM data type for this.</font>
	
## 	managements:

*	mgmttype: Constrain to one of the values in the web interface’s dropdown.  (Is there any reason not to store these in the variables table, or in a separate lookup table?  If we record units and range restrictions, this would be useful.  <font color='red'>On the other hand, if we continue to use a static list of management types, we should create a new ENUM type in the database to enumerate the allowed values.</font>
*	<font color='red'>level: This should always be non-negative (except in the case that we want to use the special value -999 for mgmttypes where a level has no meaning; if so, we should also constrain level to be non-NULL).</font>
*	units: Should be constrained to a known set of values—in fact, on a per mgmttype basis; currently there are several varying designations for the same unit in a number of cases
*	dateloc: Should be constrained to specific values.  <font color='red'>Since there is a value (9) designated as meaning "no data", this column should be constrained to be NOT NULL.  We should perhaps constraint this column to have this value if `date` is NULL.</font>
* All values of citation\_id in managements should also be associated with treatment via citations\_treatments table.  <font color='red'>Does thie mean: The management should be associated with (at least) one of the treatments associated with the citation specified by `citation_id`?</font>

##	species:

*	Ensure scientificname LIKE CONCAT(genus, ‘ ‘, species, ‘%’)
*	Ensure genus is capitalized <font color='red'>(and consists of a single word?)</font>.

## 	sites:

<font color='red'>
 *	<del>lat: range -90, 90</del>
 *	<del>lon: range -180, 180</del>
 * <ins>geometry now replaces lat, lon, and masl.  It is not clear to me what constraints (if any) can or should be placed on geometry.</ins></font>
 *	Standardize geographic names (city, country, state) using TIGER / OpenStreetMap.  
 *	use geocoding / reverse geocoding to enfoce consistency between lat, lon and city, state, country 
 *	country names should be normalized (use enum?)
*	som: 0 – 100
*	mat: range: -50, 150 
*	<font color='red'><del>masl: -100, 10,000</del> (replaced by geometry)
*	<ins>map: Minimum is zero.  Maximum = ?</ins>
*	<ins>soil: It's not clear if these should be constrained to a finite set of descriptors.  Right now the text seems somewhat free-form, but perhaps some of the information could be moved into soilnotes and this column could become an ENUM.</ins>
*	<ins>local_time: range should be -12 to +12.  This might more aptly be called timezone.  A comment should clarify the meaning; I assume it should mean something like "the number of hours local standard time is ahead of GMT".  Some kind of check might be possible to ensure consistence with the longitude.</ins>
*	<ins>sand_pct, clay_pct: These both have range 0--100, and sand_pct + clay_pct should be <= 100;
*	sitename: unique and non-null; also, ensure it does not have leading or trailing white space and no internal sequences of 2 or more consecutive spaces.  (A similar white space constraint should apply to all textual keys in all tables.)
	
## traits:

*	identify required foreign keys
*	It isn’t clear what a natural key would be, but it would probably involve several foreign key columns.  Perhaps (site_id, specie_id, cultivar_id, treatment_id, variable_id, and some combination of date and time fields.  But it is important to have some sort of uniqueness constraint other than just the default unique-id constraint.  For example, if the web-interface user accidentally presses the Create button on the New Trait page twice, two essentially equal trait rows will be created (they will differ only in the id and timestamp columns).
*	check date/time fields consistency: For example, if dateloc is 91—97, date and date_year should both be NULL (but maybe old data doesn’t adhere to this?).  If date_year, date_month, or date_day is NULL, date should be NULL as well.
*	Check mean is in the range corresponding to the variable referenced by variable_id.
*	Constraint (n, statname): For example if n =1, statname should be NULL.
*	specie_id and cultivar_id need to be consistent.
	
## treatments:

*	possibly standardize capitalization of names (easiest would be to have all words in all names not capitalized; this would convey the most information because (e.g.) author names would stand out from other words); this would need to be done manually to avoid converting proper names to lowercase
*	similarly for definitions
*	control: there can be more than one control treatment per citation (currently there are)
*	names should be unique within a citation and site pair

## users:

*	Uniqueness: login, email
*	Non-null: login, name(?), crypted_password, salt, access_level, page_access_level
	


## yields: [see also traits constraints]

* mean should be in the range of plausible yield values