---
title: 'Using Join Table : Many-to-Many Relationship'
date: 2014-10-08 16:49:10
layout: post
categories: Ruby_On_Rails
---

> You need a middle man to handle complicated relationships.

Here we have two model: **User** and **Group**. A group is like a club that members(User) can join or leave, and a user can be a member of different clubs in the same time. In order to say that relationship in Rails words, **Group has many and belongs to users, User has many and belongs to groups**, which making the table relationship to be quite complicated. The solution is to introduce join table which act as a man in the middle.

Here are three table data of **User**, **GroupMembership** and **Group**.

![many to many relationship](/assets/images/2014/10/using-join-table-many-to-many-relationship.jpg)

In Rails, User, GroupMembership and Group model are used to describe the relation.

### Model: User (app/models/user.rb)

{% highlight ruby %}
has_many :group_memberships
has_many :groups, through: :group_memberships
{% endhighlight %}

### Model: GroupMembership (app/models/group_membership.rb)

We use singular for belongs_to.

{% highlight ruby %}
belongs_to :group
belongs_to :member, class_name: "User"
{% endhighlight %}

### Model: Group (app/models/group.rb)

Notice that `foreign_key` is necessary, if not provided, Group model would auto search for `group_memberships.user_id` which does not exist.

{% highlight ruby %}
has_many :group_memberships, foreign_key: "member_id"
has_many :members, through: :group_memberships
{% endhighlight %}

### Migration: group_membership

Compound index here is used for `member_id` and `group_id`, meaning that the combination of two indexes are unique but not each of them is unique in the column.

{% highlight ruby %}
class CreateGroupMemberships < ActiveRecord::Migration
  def change
    create_table :group_memberships do |t|
      t.integer :member_id
      t.integer :group_id
      t.timestamps
    end

    add_index :group_memberships, [:member_id, :group_id], unique: true
  end
end
{% endhighlight %}
