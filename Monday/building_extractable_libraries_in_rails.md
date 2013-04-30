# Building Extractable Libraries in Rails

@patricksroberts, @iorahealth

Organizes @bostonrb

## The duality of a Rails Developer

Rubyists - Ruby is a beautiful language. We do what is beautiful and elegant. Our best practices change with our sense of beauty. Our ecosystem is driven by the many ways to solve problems.

Railsists - Rails is driven by conventions. Rails frees us from making many tedious decisions. The freedom from decisions allows us unparalleled productivity.

## /lib is the Battlefield

I believe it can benefit from some conventions.

In order to ship more code.

## Namespace All Things

E.g. No Rails Application has a User class right?? ;)

Don't do SmurfTyping.

Create a module.

```
module Smurf
  class Papa
  end
  
  class Sleepy
  end
end
```

## Avoid the Autolib Trap

Maintain explicit entry point.

Rails 3 made /lib not load by default. 

Should use initializer to require each of the libraries you need. Be specific about this.

## Use the configuration pattern

Keep credentials as far away from your library code.

```
OAUTH_KEY = '@#O$UOR#U#'   # BAD!
OAUTH_KEY - ENV['OAUTH_KEY'] # Messy!
```

But we have an initializer's directory! Pass the config in a config block.

```
module Foo
  class Configuration < Struct.new(:oauth_key)
  end
  
  class << self
    attr_accessor :configuration
  end

  def self.configure(configuration)
    self.configuration ||= configuration
  end  
end
```

## Keeping your domain models focused

Data Context Interaction.

OpenStruct - useful for test double

Mock is also usable. 

## Isolate interaction with your domain



