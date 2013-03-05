# Refinery CMS Members

Simple member engine for [Refinery CMS](http://refinerycms.com). It supports member management and page privilege setting.

This version of `refinerycms-members` supports Rails 3.2.x, RefineryCMS 2.0 and above.

## Install

Open up your `Gemfile` and add:

    gem 'refinerycms-members2'

Run `bundle install`

Next, to install the members plugin run:

    rails generate refinery:members

Note that the above task copies `*.refinery_members.rb` migration files to your `db/migrate` directory.
You should examine `*_create_members.refinery_members.rb` file and adjust it (if necessary)
to enable or disable Devise strategies and options that are appropriate for your flavor of members.

> **WARNING**: Rails 3 has a bug (fixed in Rails 4) which causes `rake railties:install:migrations`
> to copy engine migration files without a particular order. Since `refinerycms-members2`
> depends on the database table generated by `refinerycms-pages`, the migrations may be copied
> in a wrong order and thus will not run. Either start your project without `refinerycms-members2`
> and add this gem later, or rename `*.refinery_members.rb` migrations to follow
> `*_create_pages.refinery_pages.rb` migration before running `rake db:migrate` for the first time.

Finally migrate your database and you're done.

    rake db:migrate

## Testing

This section is intended for developers of refinerycms-members2.
You may skip it if you just use the gem.

Refinery-members2 uses refinery-testing gem for testing.
Follow the guidelines at http://refinerycms.com/guides/testing to setup the dummy app.
However, I couldn't get `rake spec` to work as easily as suggested at the guidelines.
If (after completing all previous steps) you find that `rake spec` does not work for you,
here's what you can do:

    cd spec/dummy
    rails g refinery:testing

At this step you should have `Guardfile` in `spec/dummy` and `spec_helper.rb` in `spec/dummy/spec`.

    rake db:test:prepare

Now we're done with the final steps of setting up the dummy app.
You can go back from `spec/dummy` to the root directory of your engine:

    cd ../..

Place your specs in `spec` directory, as usual. Run the tests as follows:

    rake spec

Apparently, one can add the finalizing steps in your `Rakefile`, by creating
`refinery:testing:setup_extension` task as suggested in `lib/refinery/tasks/testing.rake` file
of `refinery-testing` gem.

## How to build this engine as a gem

    gem build refinerycms-members2.gemspec
    gem install refinerycms-members2.gem
    
    # Sign up for a http://rubygems.org/ account and publish the gem
    gem push refinerycms-members2.gem

# Authors

  - [n5ken](https://github.com/n5ken)
  - [Slava Kravchenko](https://github.com/cordawyn)
