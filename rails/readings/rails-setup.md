# Rails Setup

There are several things you **must** do when beginning every Rails app in the near future.

## Create a New App with a Stable Version of Rails

First off, check your Rails version. In this course, we will be using Rails `>= 5.2.0`. Check to see if you have a proper version by running:

```
$ rails -v
Rails X.X.X
```

If the returns anything before `Rails 5.2.0`, run:

```
gem update rails
```

Now that you have Rails >= 5.2.0 installed, create your project with the following command:

```
# you may have a newer version of Rails installed, so make sure to specify the version
rails new my_project_name -G --database=postgresql
```
Note: Remember that the `-G` flag will prevent rails from initializing your new project as a git repository. If you want to automatically set up a repository for your project you can leave this flag off.

When using PostgreSQL, you should also run the command `bundle exec rails db:create` in the terminal before trying to run migrations.  This creates the database for your application.

[setting-up-postgresql]: https://github.com/appacademy/curriculum/blob/master/sql/readings/first-rails-project.md#postgres

## Stop the Loading of Unused Assets

In `app/views/layouts/application.html.erb`, remove the line indicated below.

```html
<%= javascript_include_tag "application" %>
```

We're not using JavaScript yet, so there's no need to load in the default JS that Rails comes with. Additionally, Rails comes with some dubious JS tricks you can use, but we want you to learn the better way. Removing the default Rails JS for now will help you get used to doing things the right way. We will tell you to put these back when we hit the JS portion of our course.


## Add Common Debugging Gems

You want to use `better_errors` and `binding_of_caller`, which will make it much easier to see what is going on in your Rails app. You also want to use `pry-rails`, which will provide a nicer console than IRB when you run `rails console`. 

```ruby
# Gemfile

group :development do
  gem 'better_errors'
  gem 'binding_of_caller'
  gem 'pry-rails'
end
```

Don't forget to `bundle install`.

**Note:** You should always place these gems in the `development` group. Rails supports three environments by default: development, test, and production. Development runs locally (`localhost:3000`). Test runs when executing RSpec tests. Production runs on sites you have deployed your app to (Heroku, www.mysweetapp.com) and are available remotely. You *never* want gems like `better_errors` or `binding_of_caller` running in production. In addition to loading unnecessary code, these gems will constitute a huge security hole if their features are exposed to the Internet. So whenever you install a new gem, think carefully about which environment(s) it is applicable to.
