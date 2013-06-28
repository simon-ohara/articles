## RSpec, Guard and Zeus

I noticed in a project using Guard for automatically running specs as they were saved that it had stopped working for some reason. There was nothing wrong with the Guardfile and I was running it under `bundle exec` to ensure I was using all of the dependencies specified in the Gemfile. Guard would start and say that it was listening but on saving a file within the watched directory none of the automgic goodness was happening.
