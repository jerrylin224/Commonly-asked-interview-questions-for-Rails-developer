# Polymorphic Association {#61da}

We use polymorphic association when we want to associate a model to more than 2 other models.

For example if you have a `Post` model and a`Video` model, and you want both of them can be commented. Instead of creating 2 join models\(`PostComment` and `VideoComment` in this example\), you can use the **polymorphic association.**

Let’s create a`Comment` table. Type the command in terminal.

```
$ rails g model Comment
```

Edit the migration file.

```ruby
class CreateComment < ActiveRecord::Migration
  def create_table :comments do |t|
    t.text :content
    t.integer :commentable_id
    t.string :commentable_type

    t.timestamps
  end
end
```

The`commentable_id`is used to store the id of the object you comment on and the`commentable_type`is used to store the type of the object\(`post`and`video`in this example.\).

But there is a shortcut can have the same effect.

```ruby
class CreateComment < ActiveRecord::Migration
  def create_table :comments do |t|
    t.text :content
    t.belongs_to :commentable, polymorphic: true
    t.timestamps
  end
end
```

Then run`db:migrate`

```
$ rake db:migrate
```

After creating our`Comment` model, we need to create the association for each model.

```ruby
class Comment < ActiveRecord::Base
  belongs_to :commentable, polymorphic: true
end

class Post < ActiveRecord::Base
  has_many :comments, as: :commentable
end

class Video < ActiveRecord::Base
  has_many :comments, as: :commentable
end
```

So if I add a comment on different post and video by using console I can see

```
post = Post.create(title: “First Post”, content: “My coding experince is…”)
=> #<Post id: 1, title: “First Post”, content: “My coding experince is…”, created_at: “2017–09–11 06:47:17”, updated_at: “2017–09–11 06:47:17”>

video = Video.create(title: “Polymorphic”, url: “https://www.youtube.com/watch?v=WOFAcbxdWjY")
=> #<Video id: 3, title: “Polymorphic”, , url: “https://www.youtube.com/watch?v=WOFAcbxdWjY", created_at: “2017–09–12 06:47:17”, updated_at: “2017–09–12 06:47:17”>

comment1 = Comment.create(commentable_id: 1, commentable_type: “Post”, content: “Interesting”)
=> #<Comment id: 1, commentable_id: 1, commentable_type: “Post”, content: “Interesting”, created_at: “2017–09–11 07:47:17”, updated_at: “2017–09–11 07:47:17”>

comment2 = Comment.create(commentable_id: 1, commentable_type: “Video”, content: “Very impressive”)
=> #<Comment id: 2, commentable_id: 3, commentable_type: “Video”, content: “Very impressive”, created_at: “2017–09–11 07:47:17”, updated_at: “2017–09–11 07:47:17”>
```

Resource: [Active Record Associations](http://guides.rubyonrails.org/association_basics.html#polymorphic-associations)

  


