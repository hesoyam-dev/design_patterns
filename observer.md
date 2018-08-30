# Observer pattern

`Define a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.`

#### Description

The Observer pattern allows you to notify parts of your program that some other part of your program has changed. It does this while allowing you to vary the objects you wish to keep informed ( observers ) from the object being observed ( the subject ) independently. It enables a highly decoupled but well informed system. Critically, you are able to add observers to a subject without having to modify either the observer or the subject.

#### Code example

```ruby
class Car
  include ServiceStation
  attr_accessor :model, :breakage
  attr_accessor :observers

  def initialize(model, breakage)
    super()
    @model    = model
    @breakage = breakage
  end
end

# observer

module ServiceStation
  def initialize
    @observers = []
  end

  def add_observer(observer)
    @observers << observer
  end

  def delete_observer(observer)
    @observer.delete(observer)
  end

  def notify_observers
    @observers.each do |observer|
      observer.update(self)
    end
  end
end

# subscribers

class Mechanic
  def update(car)
    puts "The details cost for car #{car.model} will be #{car.breakage.length * 500} USD"
  end
end

class Manager
  def update(car)
    puts "Need to offer list of details: #{car.breakage.join(',')}"
  end
end

class Owner
  def update(car)
    puts "Need to pay: #{car.breakage.length * 500}"
  end
end

#usage example
honda = Car.new("Honda Accord", ["Engine", "Windows", "Cameras", "Doors"])
mechanic = Mechanic.new
manager = Manager.new
owner = Owner.new

honda.add_observer(mechanic)
honda.add_observer(manager)
honda.add_observer(owner)

honda.notify_observers

# Result
# [Mechanic]: The details cost for car Honda Accord will be 2000 USD
# [Manager]: Need to offer list of details: Engine, Windows, Cameras, Doors
# [Owner]: Need to pay: 2000
```

### Visual example

![](https://imgur.com/uutYHND.png)
