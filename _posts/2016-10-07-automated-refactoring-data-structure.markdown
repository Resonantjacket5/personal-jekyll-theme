---
layout: post
title:  "Automated Refactoring Data Structure Draft"
date:   2016-10-01 0:00:00 -0500
tags:   thoughts
---

I've always been annoyed by the constant refactoring of simple data structures throughout by applications when the need is obvious as to what should be done in order to make my app more efficient.

For example if we have one Person and one Item and they need to reference each other then a simple reference to each would suffice:

```
Person { string name; Item owned_item;}
Item { string name; Person owner;}
```

Now if of course if we have multiple items we'll then use an array/list instead:

```
Person { string name; List<Item> owned_items;}
Item { string name; Person owner;}
```
Which is fine for most functions like: sort(), find(), as long as the number of items is small. Let's say we wanted each Person to quickly check if they own items. Then the array over time would quickly be unable to handle it as the number increases since its O(n). So we might modify it to hold a set instead.
```
Person
{
  string name;
  List<Item> owned_items;
  Set<Item> owned_items_set;
  bool check(item)
    return item in owned_items;
}
```
Now we can quickly check if the item exists in the owned_items and can still iterate over all of our owned items, though its slower than an list for that. Of course the downside is now we had to duplicate the space taken since the references are now held in both a list and a set.

Let's make it a bit harder now with a House that can hold Persons.
```
House
{
  string name;
  List<Person> renters;
}

Person{ List<Item> owned_items; etc... }
```
Let's say we have a BlueHouse = new House(); and we also had 5 Persons living in the BlueHouse with a wide assortment of items. This currently is a House-centric design as if you the reference to the BlueHouse you can find everything else, but not vice-versa. As in if I had the Person Adam, I wouldn't be able to tell where he lived nor find the object. The house on the other hand can even know what Items are inside it by proxy of looking up first he Person then all of the Items that each person has.

So if we wanted to have House.getAllPeople() or House.getAllItems() it'd be pretty fast.

Let's say we're Thomas and we want to find all Items that are type Pot in the House that owned by friends of us. So let's extend our classes again a bit focusing on the connections.
```
Person { List<Item> owned_items; List<Person> friends;}
House { List<Person> renters;}
Item { string name; string type; Person owner;}
```
The Item and the Person are connected both ways while the House connection is only one way towards the House.


















Break......

For instance if I wanted a sorting algorithm there's quicksort with O(N log N). However, if I want to be stable sort then I should use  merge sort. However, a heap sort
