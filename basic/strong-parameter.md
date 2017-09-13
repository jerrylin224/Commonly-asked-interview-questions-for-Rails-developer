# Strong parameter

With strong parameters, Action Controller parameters are forbidden to be used in Active Model mass assignments until they have been whitelisted. This means that you'll have to make a conscious decision about which attributes to allow for mass update. This is a better security practice to help prevent accidentally allowing users to update sensitive model attributes.

For example, we have a user signup form. The user need to sign up by providing `email`, `full_name` and `password`.

```ruby
%section.register.container
  .row
    .col-sm-10.col-sm-offset-1
      = bootstrap_form_for @user,
        layout: :horizontal, lablel_col: "col-sm-2", control_col: "col-sm-6", do |f|
        %header
          %h1 Register
        %fieldset
          = f.email_field :email, label: "Email Address"
          = f.password_field :password
          = f.text_field :full_name, label: "Full Name"
          = f.submit "Sign Up
```

![](/assets/螢幕截圖 2017-09-13 12.20.47.png)

When I click the `Sign Up` button, the params sent to the server will be like

```
Parameters: {
  "utf8"=>"✓",
  "authenticity_token"=>"c3K2PrBRbzzeKBSFAxK6NDi/tiMdLyDDBe5orEEh6MJ8iNNWh12332dfaersgrta9an2cfDQlyVsUfeXgZMkc8Q==",
  "user"=>{"email"=>"user@example.com",
  "password"=>"[FILTERED]",
  "full_name"=>"New User"
}
```

But actually, some malicious user can inject some content to send with the form. If we don't filter out those attributes, our important data may be affected.

For security reason, we want to only allow this 3 attributes\(`email`, `full_name` and `password`.\) to be sent to database. Therefore, we can use **strong parameter** to help whitelist which attributes should be allowed.

We sets the strong parameter in the `app/controllers/users_controller.rb` file.

```ruby
class UsersController < ApplicationController
  def create
    @user = User.new(user_params)
    if @user.save
      redirect_to root_path
    else
      render :new
    end
  end

  def user_params
    params.require(:user).permit(:email, :password, :full_name)
  end
end
```

The `require` method will ensures that a parameter is present. If it’s present, returns the parameter at the given key, otherwise raises an **ActionController::ParameterMissing error**.

```ruby
params.require(:user)
#=> {"email"=>"user@example.com", "password"=>"[FILTERED]", "full_name"=>"New User" }
params.require(:apple)
# ActionController::ParameterMissing: param is missing or the value is empty: apple
```

The `permit` method returns a new **ActionController::Parameters instance\(aka params\)** that includes only the given filters and sets the permitted attribute for the object to true. This is useful for limiting which attributes should be allowed for mass updating.

```ruby
params.require(:user).permit(:user, :password, :full_name)
#=> {"email"=>"user@example.com", "password"=>"[FILTERED]", "full_name"=>"New User" }

# Not permitted attribute won't be showed
params.require(:user).permit(:user, :password)
#=> {"email"=>"user@example.com", "password"=>"[FILTERED]" }

# You can also use permit!
params.require(:user).permit!
#=> {"email"=>"user@example.com", "password"=>"[FILTERED]", "full_name"=>"New User" }

```

Resource: [Action Controller Overview](http://edgeguides.rubyonrails.org/action_controller_overview.html#strong-parameters)







