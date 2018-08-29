# Decorator pattern

``Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.``

#### Description

Decorators allow us to add behavior to objects without affecting other objects of the same class. The decorator pattern is a useful alternative to creating sub-classes.

#### Code example
```ruby
# base class
class Car
  attr_accessor :model, :price

  def initialize(model)
    @model = model
  end

  def price
    20000
  end
end

# car with base complectation
class CarWithBaseComplectation
  attr_accessor :price

  def initialize(car)
    @car = car
  end

  def price
    @car.price += 2500
  end
end

# car with middle complectation
class CarWithMiddleComplectation
  attr_accessor :price

  def initialize(car)
    @car = car
  end

  def price
    @car.price += 5000
  end
end

# car with maximal complectation
class CarWithMaxComplectation
  attr_accessor :price

  def initialize(car)
    @car = car
  end

  def price
    @car.price += 10000
  end
end

# additional options for your car
class CarAdditionalOptions
  attr_accessor :price
  
  def initialize(car)
    @car = car
  end

  def price
    @car.price += 2000
  end
end

honda = Car.new("Honda")
max_complectation_honda = CarWithMaxComplectation.new(honda) # decorate with CarWithMaxComplectation class
max_complectation_honda_with_options = CarAdditionalOptions.new(max_complectation_honda)
puts "Final car price is: #{max_complectation_honda_with_options.price}"
```
