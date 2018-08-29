# Builder pattern

``Separate the construction of a complex object from its representation so that the same construction process can create different representations.``

#### Description

Builder pattern is useful when the algorithm how to build an object is something independent of the parts that makes the object (method that are building the object). That also defines another applicability of builder pattern: it's helpful when there can be many ways of building complex objects.

#### Code examples

###### Bad example

```ruby
  class Car
    attr_accessor :model, :type, :engine, :created, :vin_code, :color, :owner

    def initialize(model: nil, type: nil, engine: nil, created: nil, vin_code: nil, color: nil, owner: nil)
      @model    = model
      @type     = type
      @engine   = engine
      @created  = created
      @vin_code = vin_code
      @color    = color
      @owner    = owner
    end
  end

  # creating our Car
  Car.new(model: "Tesla", type: "S", engine: "electric", created: "2018-08-28", vin_code: "1FTNF20L8YEB15602", color: "wet asphalt", owner: "Oleh Budurovych")
```

There are few problems with example above:
- it doesn't look professional;
- we have very long list of parameters which limits us with the ways we can instantiate the new car;
- adding new parameter will only make situation worse;
- logic how the object build is hidden in its instantiation;

###### Good example

```ruby
class Car
  attr_accessor :model, :type, :engine, :created, :vin_code, :color, :owner
end
```
and instantiation of our car should look like this:

```ruby
  CarsBuilder.build do |builder|
    builder.set_model("Tesla")
    builder.set_type("S")
    builder.set_engine("electric")
    builder.set_creation_date("2018-08-28")
    builder.set_vin_code("1FTNF20L8YEB15602")
    builder.set_color("wet asphalt")
    builder.set_owner("Oleh Budurovych")
  end
```

CarsBuilder class will look like this:

```ruby
class CarsBuilder
  def self.build
    builder = new
    yield(builder)
    builder.car
  end

  def initialize
    @car = Car.new
  end

  def set_model(model)
    @car.model = model
  end

  def set_type(type)
    @car.type = type
  end

  def set_engine(engine)
    @car.engine = engine
  end

  def set_creation_date(created)
    @car.created = created
  end

  def set_vin_code(vin_code)
    @car.vin_code = vin_code
  end

  def set_color(color)
    @car.color = color
  end

  def set_owner(owner)
    @car.owner = owner
  end

  def car
    @car
  end
end
```

#### Conclusion

So after ```CarsBuilder``` creation we can understand what proper build parts are needed to build ```Car```.


#### Visual example

![](https://imgur.com/D7yA2RM.png)
