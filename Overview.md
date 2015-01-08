# Introduction

We are proposing implementation of database level contraints. We are consciously violating Ruby's "Active Record" approach. The [Rail Guide on Database Migrations](http://guides.rubyonrails.org/migrations.html#active-record-and-referential-integrity) suggests

> The Active Record way claims that intelligence belongs in your models, not in the database. As such, features such as triggers or foreign key constraints, which push some of that intelligence back into the database, are not heavily used.

The [manual](http://guides.rubyonrails.org/migrations.html#schema-dumping-and-you) states that ActiveRecord will not parse sql code, which is why, for example, views implemented in SQL are not encoded in Ruby's schema dump. Thus, to implement constraints, we can either a) find gems (such as [foreigner](https://github.com/matthuhiggins/foreigner) for foreign key constraints) to manage the constraints the "Ruby way" or b) move from using `db/schema.rb` to `db/structure.sql`, so that the schema is stored in SQL rather than in Ruby.

The `db/structure.sql` approach sounds simpler to me. I think that the following quote ([reference](http://ewout.name/2009/12/rails-models-with-teeth-and-database-constraints/)) sounds reasonable:

> Data tends to outlive its applications. A tight data model is a good foundation for an application and can save you a lot of trouble when migrating the data to a different system (years later). Database constraints can make your models even tighter, and enforce integrity rules that are hard to enforce in a multi-process application environment. 

Given that the Ruby web application is only one of the ways in which we use the database (e.g. we don't want to have to use the API with all of our R code ... or do we?), it seems reasonable to go with the SQL database-level constraints.

**Note SR:** To clarify these points somewhat, the foreigner gem _does_ in fact add constraints at the database level.  What it does is allow the programmer to express those foreign key constraints in Ruby code rather than in the SQL language.  It also plays nicely with schema.rb so that if adding foreign key constraints were the only consideration in choosing between db/schema.rb and db/production\_structure.rb, there would be no compelling reason to opt for the latter.

Conversely, foreigner _does not_ do anything to enforce foreign key constraints at the client application level.  It does not, for example, add any model validation code that would prevent violation of foreign-key constraints at the Ruby level and generate a user-friendly error message when a user attempts a change that would cause a violation of those constraints.

So whether we use foreigner or not and whether we switch to storing the database structure in the SQL-based db/production\_structure.rb file are largely unrelated issues.  The main reason for not using foreigner is that it requires learning (an admittedly minimal) new Ruby-based API and doesn't give us that much in return.  It would potentially allow us to continue using schema.rb to store database structure, foreign key constraints and all, but since we already have needed to switch to db/production_structure.rb to store trigger functions, this consideration is moot.

# Categories of Constraints

1.	value constraints
 *	range constraints on continuous variables
 *	“enum” constraints on, for example, state or country designations; this is a form of normalization (“US” and “USA” should be folded into a common designation); forms utilized by SELECT controls should perhaps be favored
 *	consistency constraints: for example (year, month, day) can’t be (2001, 2, 29); or city-(state)-country vs. latitude-longitude (this may be hard, but some level of checking may not be too difficult; for example, “select * from sites where country in ('US', 'United States', 'USA') and lon > 0;” shouldn’t return any rows)
2.	foreign key constraints
3.	non-NULL constraints
4.	uniqueness constraints (esp. designation of natural key)

