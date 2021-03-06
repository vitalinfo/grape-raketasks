# grape-raketasks

Rake tasks to ease the development and debugging of Grape APIs.

[![Build Status](https://travis-ci.org/reprah/grape-raketasks.svg)](https://travis-ci.org/reprah/grape-raketasks)

## Available Tasks

### Routes

`rake grape_raketasks:routes` is like `rake routes` for your Grape APIs. All routes within every Grape API in your web application will be printed to the terminal, along with parameter requiremements, HTTP verb, the API it belongs to, etc.

#### Filtering

If you want to see routes belonging to only one API:

Pass an environment variable set to your API name after writing the task. Given the API below, and assuming we only want to see routes belonging to this CatPictures API...

```ruby
module CatPictures
  class API < Grape::API
    # API stuff
  end
end
```

I'd execute `rake grape_raketasks:routes API=CatPictures::API`. Notice how we have to list which constants the API is nested in (if any), separated by a double colon, like in Ruby code.

## Installation

1.) Add `grape-raketasks` to your Gemfile:

```ruby
# Gemfile
gem 'grape-raketasks'
```

2.) Install the gem via Bundler:

```shell
$ bundle install
```
or on the command line:

```shell
$ gem install grape-raketasks
```

3.) If your Grape APIs are defined in a Sinatra or Rack web application, you need to write a rake task called `:environment`that loads the application's environment first. This gem's tasks are dependent on it. You could put this in the root of your project directory:

```ruby
# Rakefile

require 'rake'
require 'bundler'
Bundler.setup
require 'grape-raketasks'
require 'grape-raketasks/tasks'

desc 'load the Sinatra environment.'
task :environment do
  require File.expand_path('your_app_file', File.dirname(__FILE__))
end
```
Rails applications with mounted Grape APIs don't require an extra step here.

4.) Run `rake -T` to see all available rake tasks. Tasks with a `grape_raketasks` namespace should appear somewhere.

5.) Use the tasks! Find bugs or ideas for improvement! Report them here!

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Write specs for your feature
4. Commit your changes (`git commit -am 'Add some feature'`)
5. Push to the branch (`git push origin my-new-feature`)
6. Create a new pull request

## License

See LICENSE
