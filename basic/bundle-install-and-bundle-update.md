# Bundle install and bundle update

## bundle install

`bundle install`\_** **\_is a command we use to install the dependencies specified in your Gemfile.

When we run`bundle install`in a project , if there is no`Gemfile.lock`exist, Bundler will fetch all remote sources, resolve dependencies and install all needed gems.

The way Bundler resolve the dependencies is, Bundler will check the dependencies of each gem, and find out the suitable version of gem for not creating any conflict.

If`Gemfile.lock`exists, which means all the versions and dependencies of each gem is recorded. When we update a version of a gem then run`bundle install`, only the gem will be updated. But if the dependency of new version of the gem is conflicted with any other gem, the current gem won’t be updated.

Since we didn’t successfully update the gem, so the`Gemfile.lock` file will remain as the last time it was successfully updated.

### bundle update {#0c18}

What`bundle update`do is Bundler will fetch all remote sources, resolve dependencies and install all needed gems, even though there is a`Gemfile.lock`file.

You can image `bundle update` is the same as we remove the`Gemfile.lock` file and run `bundle install`.

Resource: [bundle install](http://bundler.io/v1.15/man/bundle-install.1.html)

Resource: [bundle update](http://bundler.io/v1.15/man/bundle-update.1.html)

