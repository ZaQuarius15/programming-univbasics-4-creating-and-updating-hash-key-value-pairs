# Creating and Updating Key/Value Pairs

## Learning Goals

- Update data to a `Hash` using the "bracket" method and value assignment
- Add data to a `Hash` using the "bracket" method and value assignment

## Introduction

In this lesson, we're going to look at modifying and adding data to existing
`Hash`es. This way, we can create a `Hash` then update it as we need.

## Updating Hash Values

Updating `Hash` values is very similar to looking them up. For updating, we use
the **bracket-equals** method:

```ruby
person = {
  name: "Sam",
  age: 31
}
#=> {:name=>"Sam", :age=>31}

person[:age]
#=> 31

person[:age] = 32
#=> 32

person[:age]
#=> 32
```

If we look back at the entire `Hash`, we see that the value associated with the
`:age` key has changed:

```ruby
person
#=> {:name=>"Sam", :age=>32}
```

Using the bracket-equals method, we can change any value stored inside a `Hash`.
All we need to know is the "cordinate:" the associated key.

## Adding Keys and Values to a Hash

In the previous lesson, we saw that using the bracket method and passing in an
invalid key returns `nil`:

```ruby
person[:hometown]
#=> nil
```

So, what happens when we use an invalid key with the bracket-equals method? When
Ruby discovers that the key is not present on the `Hash` in question, Ruby will
simply _create_ a key/value pair on the `Hash`:

```ruby
person = {
  name: "Sam",
  age: 31
}

# No :hometown key found
person[:hometown]
#=> nil

# Because :hometown was not present, Ruby creates the key value pair here
person[:hometown] = "Brooklyn, NY"
#=> "Brooklyn, NY"

# Now, the :hometown key refers to "Brooklyn, NY" when used in the brack method
person[:hometown]
#=> "Brooklyn, NY"

# Our original hash is also changed
person
#=> {:name=>"Sam", :age=>31, :hometown=>"Brooklyn, NY"}
```

The general syntax for adding a new value to a `Hash` is:
`hash[:new_key] = "New Value"`. `:new_key` is the literal new key we added to
the `Hash` and we assigned the `:new_key` a value of `"New Value"`.

## Update or Creating a Hash Value

We just noted that if you attempt to access a key in a `Hash` that doesn't
exist, the operation returns `nil`. Remember that `nil` is falsey in
conditions. This means we can write "update or create" logic.

First, let's take an example `Hash`:

```ruby
shipping_manifest = {
  "whale bone corset" => 5,
  "porcelain vase" => 2,
  "oil painting" => 3,
  "silverware" => 34,
  "loom" => 1
}
```

Imagine the above `Hash` is a manifest for products being shipped, with their
values representing quantity on the ship, and our job is to keep a tally as
more products are counted. A fourth "oil painting" shows up and we need to add
it to the list.  Easy enough. We'll use Ruby's "increment" expression.

```ruby
shipping_manifest["oil painting"] += 1
```

Great! But what happens when a _new_ item is introduced? Say we need to ship
one `"top hat"`, which isn't present in the `shipping_manifest` yet.

```ruby
shipping_manifest["top hat"] += 1
```

If you plug the `shipping_manifest` `Hash` into IRB and try the code snippet above,
you'll receive an error:

```text
NoMethodError (undefined method `+' for nil:NilClass)
```

Since Ruby can't find `shipping_manifest["top hat"]`.  Because of this, it
returns `nil`. As we know, Ruby doesn't like to combine data types when it
comes to operators. We are effectively writing `nil = nil + 1`, which doesn't
make any sense.

We can prevent this error from occurring by setting up a conditional and using
the bracket method to first look up a key before trying to change it:

```ruby
if shipping_manifest["top hat"]
  shipping_manifest["top hat"] += 1
else
  shipping_manifest["top hat"] = 1
end
```

Okay, so reading this in order - if `shipping_manifest["top hat"]` is truthy,
increment `shipping_manifest["top hat"]` by one. Else, assign
`shipping_manifest["top hat"]` to be equal to `1`.

Running the above conditional once again, the `"top hat"` key will be added and
set to `1`. Running it again will update `"top hat"` to `2`!

A fully professional grade implementation would probably find this logic
wrapped in a method, like so:

```ruby
def tally_item(manifest, item_name)
  if manifest[item_name]
    manifest[item_name] += 1
  else
    manifest[item_name] = 0 
  end
end

manifest = {}
tally_item(manifest, "banana")
tally_item(manifest, "highly-deadly black tarantula")
tally_item(manifest, "Mr. Tally-Man")
tally_item(manifest, "Naruto anime")
tally_item(manifest, "Darth Vader Candy")

manifest
#=> {"banana"=>2, "highly-deadly black tarantula"=>1, "Mr. Tally-Man"=>1, "Naruto anime"=>1, "Darth Vader Candy"=>2, "Leia Organa tattoo kit"=>1, "Big 6-foot, 7-foot, 8-foot bunch!"=>1}

```

## Conclusion

With the ability to update values and create entirely new key/value pairs, we've
tackled the core concepts behind Ruby `Hash`es. In the next few lessons, we will
reinforce these concepts with some lab practice.
