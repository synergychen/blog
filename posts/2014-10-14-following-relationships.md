---
title: ERD for Following Relationships
date: 2014-10-14T13:51:20+00:00
layout: post
categories: Ruby-On-Rails
---

> The logic behind `Follow` button.

Here is ERD for following model, which is the logic behind the `Follow` button. All users can follow other users as well as being followed by the others.

The goal of the relationship would be, one user as a **follower** has many users as **followed_users**, and one user at the same time could be a **followed_user** who has many **followers**. In order to clarify the relationship, we introduce a join table called **FollowingRelationship**. However, `user has many following_relationships` and `following_relationship has_many users` can't simply happen at the same time, so aliases for user and following_relationship are needed.

### User model

{% highlight ruby %}
has_many :followed_user_relationships,
  foreign_key: :follower_id,
  class_name: "FollowingRelationship"

has_many :followed_users, through: :followed_user_relationships
{% endhighlight %}

### FollowingRelationship model

{% highlight ruby %}
belongs_to :followed_user, class_name: "User"
{% endhighlight %}

### ERD

To further simplify the ERD, I split ERD above into two parts, a explanation form and an equivalent ERD model.

![erd-for-following-relationship](/assets/images/2014/10/erd-for-following-relationship.jpg)

| Name | Meaning |
| ---- | ------- |
| a_alias | follower ("fan") |
| join_alias | following_relationship |
| b_alias | followed_user ("star") |
| A | User model |
| Join | FollowingRelationship model |


Once we name all three tables with aliases, it could much easier to write the associations. Just focus on aliases.
