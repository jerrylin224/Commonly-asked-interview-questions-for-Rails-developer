# yield and content\_for

## Why use yield and content\_for

By using yield in Rails, it can help us to set some default template instead of writing duplicated code again and again. This post will simply introduce how to use \`yield\` and \`content\_for\` in your view.

## yield

The final default behavior for every action in controller are either render a template or redirect to a new route. While rendering a template, Rails will search the view in the layout first with the same controller name.

For example if the route send us to the `index` action in `User` controller, the final default order to render the template will be like:

```
app/views/layouts/user.html.erb
=> app/view/layout/application.html.erb 
=> app/view/users/index.html.erb
```

In this example we don't have the `app/views/layouts/user.html.erb`  file, so Rails will go search the `app/view/layout/application.html.erb`. Our `application.html.erb` is like



```ruby
!!! 5
%html(lang="en-US")
  %head
    %title MyFLiX - a video on demand service
    %meta(charset="UTF-8")
    %meta(name="viewport" content="width=device-width, initial-scale=1.0")
    = csrf_meta_tag
    = stylesheet_link_tag "application"
    = javascript_include_tag "application"
  %body
    %header
      = render 'shared/header'
    %section.content.clearfix
      = render 'shared/messages'
      = yield
    %footer
      &copy 2017 MyFLi
```

Within the context of a layout, yield identifies a section where content from the view should be inserted. The simplest way to use this is to have a single yield, into which the entire contents of the view currently being rendered is inserted.

In this example, the `app/view/users/index.html.erb` will be inserted into the place where yield located.

app/view/users/index.html.erb

```ruby
# app/view/users/index.html.erb
%section.user.container
  .row
    .col-sm-10.col-sm-offset-1
      %article
        %header
          %img(src="http://cdn.wpbeginner.com/wp-content/uploads/2017/08/gravatarlogo.jpg" height="40" width="40")
```

After inserted into the `layout.html.erb` will be like

```ruby
%html(lang="en-US")
  %head
    %title MyFLiX - a video on demand service
    %meta(charset="UTF-8")
    %meta(name="viewport" content="width=device-width, initial-scale=1.0")
    = csrf_meta_tag
    = stylesheet_link_tag "application"
    = javascript_include_tag "application"
  %body
    %header
      = render 'shared/header'
    %section.content.clearfix
      = render 'shared/messages'
      %section.user.container
        .row
          .col-sm-10.col-sm-offset-1
            %article
              %header
                %img(src="http://cdn.wpbeginner.com/wp-content/uploads/2017/08/gravatarlogo.jpg" height="40" width="40")
    %footer
      &copy 2017 MyFLiX
```

## content\_for

The content\_for method allows you to insert content into a named yield block in your layout. For example, we have  `app/views/layout/application.html.erb` and `app/views/users/index.html.erb`.

```ruby
# app/views/layout/application.html.erb
<html>
  <head>
    <%= yield :head %>
  </head>
  <body>
    <%= yield %>
  </body>
</html>

# app/views/users/index.html.erb
<% content_for :head do %>
  <title>A simple page</title>
<% end %>
   
<p>Hello, Rails!</p>
```

After execute the `index` action in `User` controller, the rendered html will be like

```ruby
<html>
  <head>
  <!-- Get the content from content_for :head block -->
    <title>A simple page</title>
  </head>
  <body>
  <!-- Get the content form the index.html.erb -->
    <p>Hello, Rails!</p>
  </body>
</html>
```

Resource: [Layout and rendering](http://guides.rubyonrails.org/layouts_and_rendering.html#understanding-yield)

