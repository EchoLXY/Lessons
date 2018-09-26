# Lesson 1: Intro to Ruby on Rails
Welcome! In the first lesson we'll go through the following:
1. Setup
2. Creating a new rails app
3. Parts of the app
4. Resources

## 1. Setup
First, you'll need your development environment set up. Some things you'll need: 
- Ruby
- ... + Rails (both: http://railsinstaller.org/en)
- some IDE / text editor of your choice (I recommend Sublime: https://www.sublimetext.com/3)
- Git (https://git-scm.com/downloads)
- Git Bash (needed if you have Windows only)


## 2. Creating a new rails app
To create a new rails app, change directory (cd) into your specified folder (in this case it's called workspace), run the rails command, and cd into the newly created app folder:
```bash
$ cd ~/workspace
$ rails new YOUR_APP_NAME_HERE
$ cd YOUR_APP_NAME_HERE/
```
Rails will generate a bunch of things in creating the app, including a Gemfile. To install all the gems in the Gemfile without production gems, run:
```bash
$ bundle install --without production
```

## 3. Parts of the app
### Gemfile
Rails generates a new Gemfile when you run rails new. You should have this file directly under the project directory. This is where the gems are stored. Each gem is a ruby library that extends functionality.
```ruby
source 'https://rubygems.org'

gem 'rails',        '5.1.6'
gem 'puma',         '3.9.1'
gem 'sass-rails',   '5.0.6'
gem 'uglifier',     '3.2.0'
gem 'coffee-rails', '4.2.2'
gem 'jquery-rails', '4.3.1'
gem 'turbolinks',   '5.0.1'
gem 'jbuilder',     '2.7.0'

group :development, :test do
  gem 'sqlite3', '1.3.13'
  gem 'byebug',  '9.0.6', platform: :mri
end

group :development do
  gem 'web-console',           '3.5.1'
  gem 'listen',                '3.1.5'
  gem 'spring',                '2.0.2'
  gem 'spring-watcher-listen', '2.0.1'
end

group :test do
  gem 'rails-controller-testing', '1.0.2'
  gem 'minitest',                 '5.10.3'
  gem 'minitest-reporters',       '1.1.14'
  gem 'guard',                    '2.13.0'
  gem 'guard-minitest',           '2.4.4'
end

group :production do
  gem 'pg', '0.18.4'
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
```

### app/views/layouts/application.html.erb
An embedded Ruby file for the main application page.
```html.erb
<!DOCTYPE html>
<html>
  <head>
    <title>TestApp</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```

### app/controllers/application_controller.rb
The controller for the application. Rails uses a Model-View-Controller (MVC) architechture to organize things. (Read more: https://medium.com/the-renaissance-developer/ruby-on-rails-http-mvc-and-routes-f02215a46a84)
```ruby
class ApplicationController < ActionController::Base
  protect_from_forgery with: :exception

  def hello
    render html: "hello, world!"
  end
end
```

### config/routes.rb
Routes are a Rails concept that map URLs to 
```ruby
Rails.application.routes.draw do
  root 'application#hello'
end
```
#### RESTful Routes
REpresentational State Transfer (REST) is an architectural style defined for providing standards between computer systems on the web, making it easier for systems to communicate with each other.

| HTTP Method	| What it's used for      | Examples  |
|-------------|-------------------------|-----------|
| GET	        | Retrieving a resource.	| Any time you navigate directly to a page or use google to navigating the page, you use the GET http method. |
| POST	      | Creating a resource	| Older web applications used POST for everything. |
| PUT	        | Used to completely update a resource.	| Updating your user profile on some website would typically use patch with web frameworks that support it. |
| PATCH	      | Used to partially update a resource.	| An example of this would be where you are just updating the password for your user profile. |

Source: https://richonrails.com/articles/understanding-rails-routing


## 4. Resources
### Learn Ruby!
Codecademy: https://www.codecademy.com/learn/learn-ruby

Online interactive Ruby tutorial: https://www.learnrubyonline.org/en/Welcome

### Learn Git!
Codecademy: https://www.codecademy.com/learn/learn-git

Online interactive Git branching tutorial: https://learngitbranching.js.org/
