# Gemfile and Gemfile.lock

### **Gemfile** {#374e}

Simply put, Gemfile is a format for describing gem dependencies for Ruby programs. Or you can say it contains the gems you need in this project.

### Gemfile.lock {#3151}

Gemfile.lock is a file records exact versions of all the gems you used the last time you know for sure that the application worked.

If there is error during the first time you install the gem, no`Gemfile.lock`file will be created. After you create your`Gemfile.lock`, every time you update, add or remove some gems install that, the Gemfile.lock will modify the version of the gem.

Again, if there is any error occurs while installing, the`Gemfile.lock`will not be updated and remained as the last state.

The reason `Gemfile.lock` is important is when other developers fork your project, the`Gemfile.lock` can make sure after they run bundle install, the app can run on their computers. Instead of installing the latest version of each gem then breaks the app.



Resource: [What is Gemfile](https://tosbourn.com/what-is-the-gemfile/)

Resource: [Gemfile](http://bundler.io/v1.5/gemfile.html)

