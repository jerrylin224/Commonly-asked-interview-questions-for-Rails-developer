# has\_many :through association

Many-to-many is one of the most common relationship in Rails\(database\). The concept is simple. When both 2 models have`has_many`association to each other, we say they are many-to-many relationship.

Many-to-many relationship in real life is like, a physician can have many patients, and a patient can see many different physicians.

One way to set up a many-to-many connection with another model is use`has_many :through`association. In order to do that, we need to create a new join model. We will use`Physician`,`Patient`and`Appointment`as example.

```ruby
class Physician < ApplicationRecord
  has_many :appointments
  has_many :patients, through: :appointments
end
 
class Appointment < ApplicationRecord
  belongs_to :physician
  belongs_to :patient
end
 
class Patient < ApplicationRecord
  has_many :appointments
  has_many :physicians, through: :appointments
end
```

The `Appointment` here is served as the join model. So the physician has many appointment and many patients through appointments. The patient also has many appointments and many physician to see through appointments.

### dependent {#3cc7}

How can we control the associated object when its owner is destroyed?

You can set the dependent to deal with it. The option are listed below

* :destroy causes the associated object to also be destroyed
* :delete causes the associated object to be deleted directly from the database \(so callbacks will not execute\)
* :nullify causes the foreign key to be set to NULL. Callbacks are not executed.
* :restrict\_with\_exception causes an exception to be raised if there is an associated record
* :restrict\_with\_error causes an error to be added to the owner if there is an associated object

So if you want delete the object while destroying the owner object, set dependent to destroy.

```ruby
class Physician < ApplicationRecord
  has_many :appointments, dependent: :destroy
  has_many :patients, through: :appointments
end
```

Resource: [Association Basic](http://guides.rubyonrails.org/association_basics.html#the-has-many-through-association)

