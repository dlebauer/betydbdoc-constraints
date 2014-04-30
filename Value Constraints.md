# Value Constraints

## Global

* Text fields should not have leading or trailing white spaces.
  (are there any fields for which this is not the case?)

## Covariates

*	Check level is in the range corresponding to variable referenced by variable_id.
	
## 	managements:

*	mgmttype: constrain to one of the values in the web interface’s dropdown; any reason not to store these in variables table, or in a separate lookup table? if we record units and range restrictions, this would be useful.
*	units: should be constrained to a known set of values—in fact, on a per mgmttype basis; currently there are several varying designations for the same unit in a number of cases
*	dateloc: should be constrained to specific values
* all values of citation\_id in managements should also be associated with treatment via citations\_treatments table

##	species:

*	Ensure scientificname LIKE CONCAT(genus, ‘ ‘, species, ‘%’)
*	Ensure genus is capitalized.

## 	sites:

 *	lat range -90, 90
 *	lon range -180, 180
*	Standardize geographic names (city, country, state) using TIGER / OpenStreetMap.  
 *	use geocoding / reverse geocoding to enfoce consistency between lat, lon and city, state, country 
 *	country names should be normalized (use enum?)
*	som: 0 – 100
*	mat: range: -50, 150 
*	masl: -100, 10,000
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