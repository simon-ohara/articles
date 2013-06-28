## RSpec, Guard and Zeus

I noticed in a project using Guard for automatically running specs as they were saved that it had stopped working for some reason. There was nothing wrong with the Guardfile and I was running it under `bundle exec` to ensure I was using all of the dependencies specified in the Gemfile. Guard would start and say that it was listening but on saving a file within the watched directory none of the automagic goodness was happening.

Hitting enter would run all the tests fine - but this was a manual step and I didnt want to be running the full test suite all the time.

I had a look at the docs in [the Guard README](https://github.com/guard/guard#installation) and under **Installation** it says:
>If you are on Mac OS X and have problems with either Guard not reacting to file changes or Pry behaving strange, then you should add proper Readline support to Ruby on Mac OS X.
