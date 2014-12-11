# Value Constraints (including some NOT NULL constraints)

## Global

* Text fields should not have leading or trailing white spaces. (Are there any fields for which this is not the case?)  <font color='red'><ins>
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
.</ins></font>

## covariates:

*	Check that `level` is in the range corresponding to variable referenced by `variable_id`.
*	Check that `n` is positive <font color='red'>(or > 1 ?)</font> if it is not NULL.
*	<font color='red'>Check that `statname` and `stat` are either both NULL or both non-NULL.  (Alternatively, ensure that `statname` is non-NULL and that it equals the empty string if and only if `stat` is NULL.)
*	Check that `statname` is one of "SD", "SE", "MSE", "95%CI", "LSD", "MSD" or possibly "".  Consider creating an ENUM data type for this.</font>
	
## 	managements:

*	mgmttype: Constrain to one of the values in the web interface’s dropdown.  (Is there any reason not to store these in the variables table, or in a separate lookup table?  If we record units and range restrictions, this would be useful.  <font color='red'><ins>On the other hand, if we continue to use a static list of management types, we should create a new ENUM type in the database to enumerate the allowed values.</ins></font>
*	<font color='red'>level: This should always be non-negative (except in the case that we want to use the special value -999 for mgmttypes where a level has no meaning; if so, we should also constrain level to be non-NULL).</font>
*	units: Should be constrained to a known set of values—in fact, on a per mgmttype basis; currently there are several varying designations for the same unit in a number of cases
*	dateloc: Should be constrained to specific values.  <font color='red'><ins>Since there is a value (9) designated as meaning "no data", this column should be constrained to be NOT NULL.  We should perhaps constraint this column to have this value if `date` is NULL.</ins></font>
* All values of citation\_id in managements should also be associated with treatment via citations\_treatments table.  <font color='red'>Does thie mean: The management should be associated with (at least) one of the treatments associated with the citation specified by `citation_id`?</font>

##	species:

*	Ensure scientificname LIKE CONCAT(genus, ‘ ‘, species, ‘%’)
*	Ensure genus is capitalized <font color='red'><ins>(and consists of a single word?)</ins></font>.

## 	sites:

* <font color='red'><del>lat: range -90, 90</del></font>
* <font color='red'><del>lon: range -180, 180</del></font>
* <font color='red'>geometry now replaces lat, lon, and masl.  It is not clear to me what constraints (if any) can or should be placed on geometry.</font>
* Standardize geographic names (city, country, state) using TIGER / OpenStreetMap.  <font color='red'><ins>Note that `state` is currently used not only for U.S. states, but states, regions, or provinces in other countries.  This may be harder to standardize.  (Question: Does TIGER only deal with U.S. geographic names?)</ins></font>
* use geocoding / reverse geocoding to enfoce consistency between lat, lon and city, state, country 
* country names should be normalized (use enum?)
* som: 0 – 100
* mat: range: -50, 150 
* <font color='red'><del>masl: -100, 10,000</del> (replaced by geometry)</font>
* <font color='red'>map: Minimum is zero.  Maximum = ?</font>
* <font color='red'>soil: It's not clear if these should be constrained to a finite set of descriptors.  Right now the text seems somewhat free-form, but perhaps some of the information could be moved into soilnotes and this column could become an ENUM.</font>
* <font color='red'>local_time: Range should be -12 to +12.  This might more aptly be called timezone.  A comment should clarify the meaning; I assume it should mean something like "the number of hours local standard time is ahead of GMT".  Some kind of check might be possible to ensure consistence with the longitude.</font>
* <font color='red'>sand\_pct, clay\_pct: These both have range 0--100, and sand\_pct + clay\_pct should be <= 100.</font>
* sitename: Unique and non-null (see below); also, ensure it does not have leading or trailing white space and no internal sequences of 2 or more consecutive spaces.  <font color='red'>This will make the uniqueness constraint more meaningful.</font>  (A similar white space constraint should apply to all textual keys in all tables.)
	
## traits:

*	It isn’t clear what a natural key would be, but it would probably involve several foreign key columns.  Perhaps (site_id, specie_id, cultivar_id, treatment_id, variable_id, and some combination of date and time fields.  But it is important to have some sort of uniqueness constraint other than just the default unique-id constraint.  For example, if the web-interface user accidentally presses the Create button on the New Trait page twice, two essentially equal trait rows will be created (they will differ only in the id and timestamp columns).  <font color='red'>See Uniqueness Constraints below!</font>
*	date, dateloc, time, timeloc, date\_year, date\_month, date\_day, time\_hour, time\_minute: Check date and time fields consistency: For example, if dateloc is 91—97, date and date\_year should both be NULL (but maybe old data doesn’t adhere to this?).  If date\_year, date\_month, or date\_day is NULL, date should be NULL as well.  <font color='red'><ins>Also, dateloc and timeloc should be constrained to certain meaningful values.  (See comment above on managements.dateloc.)</ins></font>
*	mean: Check mean is in the range corresponding to the variable referenced by variable_id.
*	<font color='red'>n, stat, statname: n should always be positive; if n = 1, statname should be NULL.  statname should be one of a specified set of values.  (See comments above on covariates.stat and covariates.statname.)</font>
*	<font color='red'>specie\_id and cultivar\_id need to be consistent with one another.</font>
*	<font color='red'>access_level: Range is 1--4.</font>
	
## treatments:

*	name: Possibly standardize capitalization of names (easiest would be to have all words in all names not capitalized <ins>except for proper names and unit names where appropriate</ins>; this would convey the most information because (e.g.) author names would stand out from other words).  This would need to be done manually to avoid converting proper names to lowercase.  <font color='red'><ins>As stated below, names should be unique within a citation and site pair; standardizing capitalization will make this constraint more meaningful.</ins></font>
*	definition: Treat captitalization similarly to that for names.
*	control: There can be more than one control treatment per citation (currently there are).  <font color='red'>Below in the uniqueness section, it is stated that there can be only one control for a given citation _and site_.</font>
*	Since (as stated below) names should be unique within a citation and site pair, standardizing capitalization will make this constraint more meaningful.

## users:

*	<del>Uniqueness: login, email</del> [See Uniqueness section below.]
*	<del>Non-null: login, name(?), crypted_password, salt, access_level, page_access_level</del> [See Non Null section below.]
*	<font color='red'>login: Enforce any constraints required by the Rails interface.</font>
*	<font color='red'>email: Constrain to valid email addresses.</font>
*	<font color='red'>country: Constrain to valid country names.</font>
*	<font color='red'>area: This currently isn't very meaningful.  Perhaps this should be an ENUM.  Alteratively, it could be constraint to be some category word followed by free-form text.</font>
*	<font color='red'>access\_level: Range is 1 - 4.</font>
*	<font color='red'>page\_access\_level: Range is 1 - 4.</font>
*	<font color='red'>postal\_code: Ideally, this should be constrained according to the country.  Since most users are (currently) from the U.S., we could at least constraint U.S. postal codes to "NNNNNN" or "NNNNNN-NNNN".</font>
	


## yields: [see also traits constraints]

* mean: mean should be in the range of plausible yield values.