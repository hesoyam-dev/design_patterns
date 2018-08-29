# Adapter Pattern

``Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.``

#### Description

The Adapter pattern is specifically designed to deal with one system which has to interface with an already existing system in which a common interface between the two systems is desired.

#### Code example
```ruby
# The Car class, acts as and 'adaptee'
# It has an existing interface, which we want
# to adapt to a common, 'BoostedCar' interface
class Car
  attr_accessor :engine, :turbine

  def drive
    @engine.start
    @engine.exec
    # code implementation for driving a car
  end

  def boost!
    puts "Vroom vroom!"
    @turbine.exec
  end
end

# The CarAdapter is 'adapter' between Car ('adaptee') and
# BoostedCar ('target') classes. Acts as adapter!
class CarAdapter
  attr_accessor :car

  def initialize(car)
    @car = car
  end

  def use_turbine
    @car.boost!
  end
end

# The BoostedCar class is our 'target' class
# interface that we want to use within our system
class BoostedCar

  def initialize(adapter)
    @adapter = adapter
  end

  def use_turbine
    @adapter.use_turbine
  end
end

# In our app implementation we initialize a Car class
# pass it to a Car adapter, and then pass the Car adapter into our 'target'
# an instance of BoostedCar class

car = Car.new
car_adapter = CarAdapter.new(car)
boosted_car = BoostedCar.new(car_adapter)

# Finally we can use 'use_turbine' method to boos our car
boosted_car.use_turbine

```

### Visual example

![](https://i.imgur.com/YxzcMra.png)

![](https://imgur.com/YuL7PIm.png)
