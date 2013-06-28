## RSpec, Guard and Zeus

I noticed in a project using Guard for automatically running specs as they were saved that it had stopped working for some reason. There was nothing wrong with the Guardfile and I was running it under `bundle exec` to ensure I was using all of the dependencies specified in the Gemfile. Guard would start and say that it was listening but on saving a file within the watched directory none of the automagic goodness was happening.

Hitting enter would run all the tests fine - but this was a manual step and I didnt want to be running the full test suite all the time.

I had a look at the docs in [the Guard README](https://github.com/guard/guard#installation) and under **Installation** it says:
>If you are on Mac OS X and have problems with either Guard not reacting to file changes or Pry behaving strange, then you should add proper Readline support to Ruby on Mac OS X.

So it seems that somewhere down the line either in an update of OSX or Guard the dependency for Readline has either been created or broken. I also noticed through my search for a solution to this that [guard-rspec](https://github.com/guard/guard-rspec) now has support for [zeus](https://github.com/burke/zeus) which would help the automation be even quicker!

Heres what I did:

First of all make sure XCode is up-to-date in the AppStore.

Then make sure brew is up-to-date and then install Readline

```bash
brew update
brew install readline
```
**NB** Im using ruby 1.9.3-p0 under rbenv with ruby-build already installed. If your setup is not like this then I suggest you read [the more detailed instructions for installing Readline](https://github.com/guard/guard/wiki/Add-Readline-support-to-Ruby-on-Mac-OS-X)


Now add in the gems to the `:development` group of your Gemfile.
```ruby
group :development, :test do
  gem "rb-readline"
  gem "zeus"
  #
  # other gems
  #
end
```

Then adjust your Guardfile to make use of Zeus:

add zeus to spec options:

guard 'rspec', :all_on_start => false, :all_after_pass => false, :zeus => true do

:wqa

bundle

new term window => zeus start

be guard
