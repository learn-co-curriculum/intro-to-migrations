# Active Record Migrations

## Objectives

1. Understand the usefulness of using migrations to effect changes to your database. 
2. Learn how to write migrations to apply any kind of change to your database. 

## What are Migrations?

From the very excellent Rails Guides:

>Migrations are a feature of Active Record that allows you to evolve your database schema over time. Rather than write schema modifications in pure SQL, migrations allow you to use an easy Ruby DSL to describe changes to your tables.
> –– [Rails Guides, Active Record Migrations](http://edgeguides.rubyonrails.org/active_record_migrations.html)

To put it plainly, migrations allow us to quickly and easy write and execute Ruby code that will apply changes to our database. Anything from creating and dropping tables to altering table structure (adding/removing columns, changing the name or data types of columns, etc). 

## Why use Migrations?

One of the goals of using Active Record is to write less SQL. (This is an admirable goal, I'm sure you'd agree.) Using tools like the SQLite-Ruby gem, we can wrap many of our database interactions in Ruby methods. For example:


```ruby
database_connection = SQLite::Database.new("path-to-my-database")

database_connection.execute("CREATE TABLE cats (id INTEGER PRIMARY KEY, name TEXT, age INTEGER)")
```

With this technique, we can add a column to our cats table pretty easily:

```ruby
database_connection.execute("ALTER TABLE cats ADD COLUMN breed TEXT")
``` 

You can see that in order to apply changes to our database, we write a combination of Ruby and SQL. To make these changes, such as creating a new table or changing that table, we will end up writing the same (or very similar) lines of code again and again. 

As programmers we hate repetition. Luckily for us, the makers of Active Record recognized this repetition and provided us with a tool that allows us to write database changes in Ruby and execute them quickly and easy––migrations.

Migrations have the added benefit of allowing us to track changes to our database. We might write one migration that creates a certain table and another migration that changes that table later on. So, each migration becomes a list of changes to our database. We can refer to this list at any time, we can even apply particular changes and not others, or reverse particular changes and not others. It's like version control for our database!

