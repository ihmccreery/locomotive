Locomotive
===

A guide to setting up a rails app, from zero to deployed, with some common components

A few notes before we begin
---

I won’t be telling you when to check in changes to Git.  Figure it out yourself.  I recommend doing it often. 

The basics
---

Create an empty GitHub repository: <http://github.com/new>.

Clone it:

    $ git clone git@github.com:ihmccreery/locomotive.git

Initialize a Rails project:

    $ cd locomotive/
    $ rails new .

Change the README to Markdown:

    $ git rm README.rdoc
    $ touch README.md

At this point, all things should be good in the world:

    $ rails server

PostgreSQL
---

Let's make some databases.

First off, let's get something straight.  Use PostgreSQL.  Just do it.  If you don't already have PostgreSQL running, and you're on OS X, I recommend [Postgres.app](http://postgresapp.com).

In your `Gemfile`:

    # Use PostgreSQL as the database for Active Record
    gem 'pg'

Your `config/database.yml` should look like this:

    development:
      adapter: postgresql
      encoding: unicode
      host: localhost
      database: locomotive_dev
      pool: 5

    # Warning: The database defined as "test" will be erased and
    # re-generated from your development database when you run "rake".
    # Do not set this db to the same as development or production.
    test:
      adapter: postgresql
      encoding: unicode
      host: localhost
      database: locomotive_test
      pool: 5

Make some databases:

    $ createdb locomotive_dev
    $ createdb locomotive_test

Run the initial migration to create a schema:

    $ rake db:migrate

That's it for now!

Testing
---

Let's use RSpec.  First thing, get rid of Test::Unit:

    $ git rm -r test/

And install [rspec-rails](http://github.com/rspec/rspec-rails), [Machinist](http://github.com/notahat/machinist), and [Capybara](http://github.com/jnicklas/capybara):

    # Use RSpec for testing
    group :development, :test do
      gem 'rspec-rails'
      gem 'machinist'
      gem 'capybara'
    end

And follow these guides:

- `rspec-rails`: <http://github.com/rspec/rspec-rails#installation>
- `machinist`: <http://github.com/notahat/machinist#installation>
  - I recommend using `fixture_replacement`
- `capybara`: <http://github.com/jnicklas/capybara#setup>
