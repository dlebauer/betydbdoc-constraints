## Categories of Constraints

1.	value constraints
 *	range constraints on continuous variables
 *	“enum” constraints on, for example, state or country designations; this is a form of normalization (“US” and “USA” should be folded into a common designation); forms utilized by SELECT controls should perhaps be favored
 *	consistency constraints: for example (year, month, day) can’t be (2001, 2, 29); or city-(state)-country vs. latitude-longitude (this may be hard, but some level of checking may not be too difficult; for example, “select * from sites where country in ('US', 'United States', 'USA') and lon > 0;” shouldn’t return any rows)
2.	foreign key constraints
3.	non-NULL constraints
4.	uniqueness constraints (esp. designation of natural key)
