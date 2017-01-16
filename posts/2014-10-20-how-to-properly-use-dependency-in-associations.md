---
title: How to Properly Use Dependency in Associations
date: 2014-10-20T12:51:08+00:00
layout: post
categories: Ruby-On-Rails
---
> Live and die together.

Why do we need dependency in our associations? Delete dependent and redundant data to make database clean.

Let's start with an example. Assume we have three models, **User**, **Gallery** and **Image** with the following relationships and a database table

- a user has many galleries
- a gallery has many images
- a gallery belongs to a user
- a image belongs to a gallery

![dependency-in-association](/assets/images/2014/10/how-to-properly-use-dependency.jpg)

And for some reason we want to delete user `id = 2`;. Without dependency, this user would be deleted while galleries with `user_id = 2` and images with `gallery_id = 1 & 4` still remain in database. However, in practical case, we do want delete all its dependencies to clean the database.

The power of Rails is that instead of

{% highlight ruby %}
class User < ActiveRecord::Base
  has_many :galleries
end

class Gallery < ActiveRecord::Base
  has_many :images
  belongs_to :user
end

class Image < ActiveRecord::Base
  belongs_to :gallery
end
{% endhighlight %}

you could simply add `dependent: :destroy` to Active Record Association to delete all dependencies.

{% highlight ruby %}
class User < ActiveRecord::Base
  has_many :galleries, dependent: :destroy
end

class Gallery < ActiveRecord::Base
  has_many :images, dependent: :destroy
  belongs_to :user
end

class Image < ActiveRecord::Base
  belongs_to :gallery
end
{% endhighlight %}

Now if you delete user `id = 2`

{% highlight ruby %}
User.find(2).destroy
{% endhighlight %}

galleries with `id = 1, 4` and images with `id = 1, 2, 4, 6` would all be deleted.

Notice that we must not add dependent to both has_many and belongs_to in the same time, such as follows. Once you add dependent to all associations, it would get you into an infinite loop of **delete a user => find and delete the user's associated gallery => find delete the gallery's associated user**.

{% highlight ruby %}
class User < ActiveRecord::Base
  has_many :galleries, dependent: :destroy
end

class Gallery < ActiveRecord::Base
  has_many :images, dependent: :destroy
  belongs_to :user, dependent: :destroy
end

class Image < ActiveRecord::Base
  belongs_to :gallery, dependent: :destroy
end
{% endhighlight %}
