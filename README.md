# Working with Legislator Data

## Summary
This challenge represents a fairly comprehensive reflection of our object-oriented programming, schema design, and Active Record abilities.  The challenge is to build a command line application that allows us to interact with data on U.S. legislators pulled from the [Sunlight Foundation][].

We'll be given descriptions of required features for our application, but we'll need to decide how to build out that functionality.  What types of objects do we need?  What about views and controllers?  How will users enter commands, command line arguments?  Leverage the learning from the past few weeks to make reasoned choices.


### Active Record Query Interface
We should be familiar with the more common Active Record query methods like `.all`, `.find`, and `.where`.  To complete this challenge, it will be helpful to also be familiar with some more advanced portions of [Active Record's query interface][AR Query Interface].  For example, [eager loading][] where we load an object with its associated objects.  We can define [scopes][Scopes] to return subsets of a class's records.  If it's possible that a record might already exist in the database, we can first [try to find it and then build or create it][Find or Build] if it's not there.  There are powerful features built into Active Record, and we need to learn to use them.


## Releases
### Pre-release: Preparation
Take a minute to get acquainted with the provided code base.  To run our application, we'll execute the `runner.rb` file.  This file requires `config/environment.rb` which more-or-less requires everything else we'll need.

Before moving on, let's bundle and create our database.


### Release 0:  Seed the Database
We have data from the Sunlight Foundation's Congress API on everyone who's served in the U.S. Congress (see `db/data/legislators.csv`).  We need to get that data into our database.  This means that we need to design a database schema to hold the data.  Then we need to write and run migrations to create the tables in our database.  And finally, we need to import the data in the CSV file into our database.

Write the script for importing the data in the `db/seeds.rb` file.  Keep in mind that when we receive data, it is not guaranteed to be in perfect order, so we might want or need to *scrub* the data.  For example, we'll need to account for some legislators having no birthday.  And some political parties are denoted with an abbreviation (e.g. "I" for Independent) while others have the full party name provided (e.g. "Whig").

*Hint:*  In designing the schema, consider all the data in a single row of the CSV file; there's data on the legislator, the represented state, and the political party.  Also, read through the releases, so you'll know what the expectations are.  


### Release 1:  Display Legislators in Office
Now that we have data in our database, let's build the application to interact with it.  We'll start by allowing users to display a list of legislators who are currently in office.  The output should include the legislators' full names including title and suffix.  A sample of output might look like Figure 1.

*Hint:*  This is a good opportunity to define a [scope][Scopes]—maybe we allow ourselves to call something like `Legislator.in_office`.

```
Rep. Diane Black
Sen. Maria Cantwell
Sen. Sherrod Brown
```
*Figure 1*.  Example of how a list of legislators might be formatted.


### Release 2: Display Legislators Born Between Two Dates
Add a feature that allows users to display a list of legislators who were born between two dates.  For example, legislators born between June 1, 1936 and December 31, 1936.  The output should include the legislators' full names including title and suffix, just as in *Release 1*.

*Hint:* You can pass a [range condition][] to `.where`.


### Release 3: Combine In-office and Born-between
We can display a list of legislators that are in office and a list of those born within a date range.  Combine the two, so that users can display a list of legislators who are both in office and born between two dates.  The output should include the legislators' full names including title and suffix, just as in *Releases 1 - 2*.

*Hint:* Scopes are chainable.


### Release 4: Update the Legislator List Display
Let's change how our lists are displayed.  In addition to a legislator's name, display the legislator's state abbreviation and political party (see Figure 2).  This change should affect the display for *Releases 1 - 3*.

*Hint:*  [Eager loading][] helps us efficiently query the database for associated objects—for example, loading legislators with their states and parties.

```
Rep. Diane Black (TN, Republican)
Sen. Maria Cantwell (WA, Democratic)
Sen. Sherrod Brown (OH, Democratic)
```
*Figure 2*.  Example of how an updated list of legislators might be formatted.

### Release 5: List States/Territories Represented in Congress
Puerto Rico; Washington, D.C.; and other territories are represented in Congress alongside the 50 states.  Add a feature that allows users to list all the states and territories that have been represented in Congress.  Order the list alphabetically by state abbreviation.  Include the state abbreviation and the counts of in-office senators and representatives (see Figure 3).

```
AK:  2 Senators, 1 Representatives
AL:  2 Senators, 7 Representatives
AR:  2 Senators, 4 Representatives
AZ:  2 Senators, 9 Representatives
```
*Figure 3*.  Example of how a list of states might be formatted.


### Release 6:  Display the Active Legislators for a State
Users can display a list of states and how many legislators serve each state in Congress.  Add a feature that allows users to display the list of an individual state's legislators—for example, Ohio's legislators currently serving in Congress (see Figure 4).

Here are the requirements for the feature.

- List only in-office legislators.
- Senators should be listed before representatives.
- Alphabetize the lists of senators and representatives by last name.
- Identify legislators by party.

```
Senators:
  Sherrod Brown (D)
  Robert J. Portman (R)
Representatives:
  Joyce Beatty (D)
  Steve J. Chabot (R)
  Warren Davidson (R)
  
  list continues ...
```
*Figure 4*.  Example of how the list of Ohio's legislators might be formatted.


## Conclusion
This challenge forces us to apply much of what we've covered at Dev Bootcamp: how to organize our code, schema design, Active Record, etc.  We were also directed to look at some more advanced Active Record features.  

Take a few minutes to reflect on this challenge.  How did it feel?  Did we know when to apply a concept?  Did we struggle with how to approach a problem?  Or how to implement a decision?  What did we do well?  Where could we use improvement?  What can we do to sharpen our understanding and skills as we transition from building command line applications to building web applications?


[AR Query Interface]: http://guides.rubyonrails.org/v4.2/active_record_querying.html
[Eager Loading]: http://guides.rubyonrails.org/v4.2/active_record_querying.html#eager-loading-associations
[Find or Build]: http://guides.rubyonrails.org/v4.2/active_record_querying.html#find-or-build-a-new-object
[range condition]: http://guides.rubyonrails.org/active_record_querying.html#range-conditions
[Scopes]: http://guides.rubyonrails.org/v4.2/active_record_querying.html#scopes
[Sunlight Foundation]: https://sunlightfoundation.com/

