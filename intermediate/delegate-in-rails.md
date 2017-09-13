# delegate

`delegate`  provides a delegate class method to easily expose contained objects’ public methods as your own. Simply say, through delegation you can use public methods in other model directly.

For example I have a `QueueItem` and a`Video` model.

```ruby
QueueItem < ActiveRecord::Base
  belongs_to :video
end

Video < ActiveRecord::Base
  has_many :queue_items
  belongs_to :category
end
```

If I want to get the category object of the video in first queue\_item, I may write

```ruby
queue_item = QueueItem.first
queue_item.video.category.name
#=> "Action"
```

It is kind of cumbersome. Instead of getting the object via model association, we can use delegate to help us.

```ruby
class QueueItem < ActiveRecord::Base
  belongs_to :video
 
  delegate :category, to: :video
end
```

Then we can get the category by

```ruby
queue_item = QueueItem.first
queue_item.category.name
#=> "Action"
```

Or even you can set a`category_name`method in the `QueueItem`model.

```ruby
class QueueItem < ActiveRecord::Base
  belongs_to :video
 
  delegate :category, to: :video
  def category_name
    category.name
  end
end

queue_item = QueueItem.first
queue_item.category_name
#=> "Action"
```

You can set one or more method names \(specified as symbols or strings\) if you want. And the name of the target object via the `:to`option\(also a symbol or string\).

There are some options you can use in `delegation` .

* :to — Specifies the target object
* :prefix — Prefixes the new method with the target name or a custom prefix
* :allow\_nil — if set to true, prevents a NoMethodError to be raised

You can use the `prefix` option to make the method more readable.

```ruby
class QueueItem < ActiveRecord::Base
  belongs_to :video
  delegate :category, to: :video
  delegate :title, to: :video, prefix: :video
end

queue_item = QueueItem.first
queue_item.video_title == queue_item.video.title
# => true
```

Resource: [rails/Module/delegate](https://apidock.com/rails/Module/delegate)

