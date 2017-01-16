---
title: '!! ( not not ) in JavaScript'
date: 2015-04-22T20:15:58+00:00
layout: post
categories: JavaScript
---

> You know me if you know `!`.

`!!` (not not) is just `!` (not) twice, to coerce `object` to `boolean`.

### When does !! return false?

1. `undefined`
2. `""` (empty string)
3. `false` (boolean)
4. `0`
5. `null`
6. `NaN`

### When does !! return true?

All except above 6 cases.
