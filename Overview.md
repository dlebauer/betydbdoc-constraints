# Introduction

We are proposing implementation of database level contraints. We are consiously violating Ruby's "Active Record" approach. The [Ruby manual](http://guides.rubyonrails.org/migrations.html#active-record-and-referential-integrity) suggests

> The Active Record way claims that intelligence belongs in your models, not in the database. As such, features such as triggers or foreign key constraints, which push some of that intelligence back into the database, are not heavily used.

The [manual](http://guides.rubyonrails.org/migrations.html#schema-dumping-and-you) states that ActiveRecord will not parse sql code, which is why views implemented in SQL are not encoded in Ruby's schema dump. We can either implement constraints either by a) find gems (such as [foreigner](https://github.com/matthuhiggins/foreigner) for foreign key constraints) to manage the constraints the "Ruby way" or b) move from using `db/schema.rb` to `db/structure.sql`, so that the schema is stored in sql rather than ruby.

The `db/structure.sql` approach sounds simpler to me. I think that the following quote ([reference](http://ewout.name/2009/12/rails-models-with-teeth-and-database-constraints/)) sounds reasonable:

> Data tends to outlive its applications. A tight data model is a good foundation for an application and can save you a lot of trouble when migrating the data to a different system (years later). Database constraints can make your models even tighter, and enforce integrity rules that are hard to enforce in a multi-process application environment. 

Given that the Ruby web application is only one of the ways in which we use the database (e.g. we don't want to have to use the API with all of our R code ... or do we?), it seems reasonable to go with the SQL database level constraints.

# Categories of Constraints

1.	value constraints
 *	range constraints on continuous variables
 *	“enum” constraints on, for example, state or country designations; this is a form of normalization (“US” and “USA” should be folded into a common designation); forms utilized by SELECT controls should perhaps be favored
 *	consistency constraints: for example (year, month, day) can’t be (2001, 2, 29); or city-(state)-country vs. latitude-longitude (this may be hard, but some level of checking may not be too difficult; for example, “select * from sites where country in ('US', 'United States', 'USA') and lon > 0;” shouldn’t return any rows)
2.	foreign key constraints
3.	non-NULL constraints
4.	uniqueness constraints (esp. designation of natural key)

