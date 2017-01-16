---
layout: post
title: Understanding Rails Concerns
date: 2017-01-08 13:27:00
categories: Rails
---

> It's all about DRYing your model and grouping functionalities.

Concerns is basically a module to DRY model.

### Why Using Concerns

When you feel uncomfortable with code duplication across different models, you need to concern `concerns`.

Assume we have model `Picture`, `Person` and `Product`:

```ruby
class Picture < ActiveRecord::Base
  belongs_to :imageable, polymorphic: true
end

class Person < ActiveRecord::Base
  has_many :pictures, as: :imageable
  
  def lastest_photo
    ...
  end
  
  def self.total_photos
    ...
  end
end

class Product < ActiveRecord::Base
  has_many :pictures, as: :imageable
  
  def lastest_photo
    ...
  end
  
  def self.total_photos
    ...
  end
end
```

Code smell might gently poke you saying that following piece of code is duplicated for `Person` and `Product`:

```ruby
has_many :pictures, as: :imageable

def lastest_photo
  ...
end

def self.total_photos
  ...
end
```

Let DRY it by extracting to a module.

With considering `DRY` + `Module`, Rails 4 officially introduces `Concerns`.

### How to Use Concerns

Concerns comes to rescue. Here's how:

```ruby
class Picture < ActiveRecord::Base
  belongs_to :imageable, polymorphic: true
end

class Person < ActiveRecord::Base
  include imageable
end

class Product < ActiveRecord::Base
  include imageable
end

# app/models/concerns/imageable.rb
module Imageable
  extend ActiveSupport::Concern
  
  included do
    has_many :pictures, as: :imageable
  end
  
  def lastest_photo
    ...
  end
  
  module ClassMethods
    def total_photos
      ...
    end
  end
end
```

### What's New About Concerns

Creating a concerns is much the same as creating a module except:

##### File Location

Rails create a VIP room under its convention to hold all concerns, which is `app/models/concerns/`.

##### More Than A Module

Concerns would notify module that "we are special and more than a module" by `extend ActiveSupport::Concern`.

### How to Test Concerns

With the help of `shared example group`, testing concerns is easiler. It basically let user to describe behaviour of a module.

```ruby
# spec/concerns/imageable_spec.rb
require 'spec_helper'

shared_examples_for "imageable" do
  let(:model) { described_class }

  ...
end

# spec/models/person_spec.rb
require 'spec_helper'
require Rails.root.join "spec/concerns/imageable_spec.rb"

describe Person do
  it_behaves_like "imageable"
end

# spec/models/product_spec.rb
require 'spec_helper'
require Rails.root.join "spec/concerns/imageable_spec.rb"

describe Product do
  it_behaves_like "imageable"
end
```

`described_class` might be confusing unless combining it with each mode spec examples.

By making argument of `describe` example be a class name, in our case, `describe Person` and `describe Product`, we made `model` being accessible as `Person` and `Product` under each `describe` examples.
