## RSpec, Guard and Zeus

I noticed in a project using Guard for automatically running specs as they were saved that it had stopped working for some reason. There was nothing wrong with the Guardfile and I was running it under `bundle exec` to ensure I was using all of the dependencies specified in the Gemfile. Guard would start and say that it was listening but on saving a file within the watched directory none of the automagic goodness was happening.

Hitting enter would run all the tests fine - but this was a manual step and I didnt want to be running the full test suite all the time.

I had a look at the docs in [the Guard README](https://github.com/guard/guard#installation) and under **Installation** it says:
>If you are on Mac OS X and have problems with either Guard not reacting to file changes or Pry behaving strange, then you should add proper Readline support to Ruby on Mac OS X.

So it seems that somewhere down the line either in an update of OSX or Guard the dependency for Readline has either been created or broken. Heres how I rectified it:

###Adding Readline Support

First of all make sure XCode is up-to-date in the AppStore.

Then make sure brew is up-to-date and then install Readline

```bash
brew update
brew install readline
```
**NB** Im using ruby v1.9.3-p0 under [rbenv](https://github.com/sstephenson/rbenv) with [ruby-build](https://github.com/sstephenson/ruby-build#installing-with-homebrew-for-os-x-users) already installed. If your setup is not like this then I suggest you read [the more detailed instructions for installing Readline](https://github.com/guard/guard/wiki/Add-Readline-support-to-Ruby-on-Mac-OS-X)


Now add in the gems to the `:development, :test` group of your Gemfile.
```ruby
group :development, :test do
  gem "rb-readline"
  #
  # other gems
  #
end
```

Run `bundle` then `guard` and you should notice the automagic has returned when editing a spec file or the file that it is testing.

```bash
bundle
bundle exec guard
```

###Hooking into Zeus

I also noticed through my search for a solution to this that [guard-rspec](https://github.com/guard/guard-rspec) now has support for [zeus](https://github.com/burke/zeus) which would help the automation be even quicker!

First, exit Guard if you already have it running
```bash
[1] guard(main)> e
```

Guard works from your Gemfile dependencies so Zeus needs to be referened there, even though you may have Zeus installed globally.
```ruby
group :development, :test do
  gem "rb-readline"
  gem "zeus"
  #
  # other gems
  #
end
```

Adjust your Guardfile to harness Zeus by switching on the option in guard-rspec:
```ruby
guard 'rspec', :zeus => true do
  #
  # Various guard directives
  #
end
```

In one term window start the Zeus server
```bash
zeus start
```

Then, in anohter term window run Guard as normal
```bash
bundle exec guard
```

This will allow each test to run automatically after saving without having to boot up the rails app in the background each time.
