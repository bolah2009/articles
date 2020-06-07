# Understanding Variables in Ruby

Variables are representation of objects in ruby, when `name = ‘Bola’`, `name` in ruby is a type of variable that is associated with the string `’Bola’`. We can modify and reuse variables, this makes them valuable. See examples below:

```rb
first_name = 'Bola'
last_name = 'Buari'
full_name = "#{first_name} #{last_name}"
```

Although the example above is a basic one, however, we see that the variable is been reused rather than been re-assigned.

## Types of Variables

Unlike some other programming languages, the type of variables defines its modifiability and scope. In ruby, there are three types of variables, a constant and some pseudo-variables (strictly two).

- Local Variables, starts with lower case a-z or underscore (\_).
- Global Variables, starts with \$.
- Instance Variables starts with @.
- Constant, starts with upper case A-Z.
- Pseudo-variables

### Local Variables

A local variable scope is inside a method, class, module, proc or loop block, and if it’s in none, then its scope is in the tire program/file. This implies that a variable defined inside a method can not be used outside such a method, the same applies to other blocks.

See examples below:

```rb
name = 'Bola'
print name
# 'Bola' (output)
```

Defining a variable inside a procedure object is scoped only to the proc

```rb
p = proc { temp_name = 'Ahmed'; print temp_name}
p.call
# Ahmed (output)
```

Trying to access such variable outside of its scope will result in an error `(NameError)`

```rb
print temp_name
# undefined local variable or method `temp_name' for main:Object (NameError)
```

However, local variables that are outside but in the same scope with a procedure object can be used inside such procedure object

```rb
last_name = 'Buari'

p = proc { print last_name}
p.call
# Buari (output)
```

This is also true for other blocks like a `loop` block

```rb
loop { print last_name; break}
# Buari (output)
```

But not for a method block, as we get an error, which means a local variable in the same scope with a method, is not accessible in such a method.

```rb
def print_name
 print last_name
end

print_name
# undefined local variable or method `last_name' for main:Object (NameError)
```

The `defined?` method is good for printing the type of variable a variable is we can see that from the output below the type of variable the following is:

```rb
name = "Bola"
p defined? name
# "local-variable"
```

### Global Variables

Global variables start with the `$` symbol, unlike local variables, it does not need to be assigned a value before they can be called, this means that calling an unassigned global variable gives the `nil` value instead of an error. See below:

```rb
# Local varible raised an error
p new_variable
# undefined local variable or method `new_variable' for main:Object (NameError)

# Global variable outputs nil
p $new_variable
# nil (output)
```

The major feature about a global variable is that it is used everywhere in the program/file irrespective of the scope. See examples:

The below example shows how global example is defined outside of a method but acmes in that method.

```rb
$last_name = 'Buari'

def print_name
    p $last_name
end

print_name
# Buari (output)
```

Another example is assigning a value to a global variable inside a method but accessing the value outside, but note that the method has to be called such value to be defined, else we will have `nil`, a default value of an unassigned global variable.

```rb
def print_name
   $first_name = 'Bola'
end

p $first_name
# nil (output)
```

It outputs nil as excepted as the method that assigned a value to it has not been called. Now, let’s call the method and check the value of `$first_name` again.

```rb
print_name
p $first_name
# Bola (output)
```

Now we have `Bola` as excepted.

Let’s note that since global variables are scoped everywhere in the program, using the same name in a different scope like a method, changes the value for the global variable when this method is called. See example:

```rb
age = 30

def change_age
    age = 50
end

change_age

p age
# 30 (output)

```

First, we use a local variable as an example, above is a local variable `age` assigned the value `30`, but assigning another local variable `age` inside the method `change_age` did not affect the local variable `age` declared in the outer scope. Now let’s check out below for a global variable

```rb
$age = 30

def change_age
    $age = 50
end

change_age

p $age
# 50 (output)

p defined? $age
# "global-variable" (output)
```

As we can see, unlike the local variable the initial assignment was affected when the `change_age` method is called, as it reassigned another value to the `$age` global variable. Also, using the method `defined?` shows that it’s a global variable.

### Instance Variables

Instance variables start with the symbol `@`. Like global variables that are also instantiated with the `nil` value if no value has been assigned.

The instance variable is scoped to the object `self`, this means that if two different objects `p1` and `p2` belongs to the same class `Person`, their instance variable from `Person` class can be different.

Let’s examine the class defined below with three instance variables (`@first_name`, `@ last_name`and `@ full_name`):

```rb
class Person
  def set_first_name(name)
    @first_name = name
  end

  def set_last_name(name)
    @last_name = name
  end

  def full_name
    @full_name = "#{@first_name} #{@last_name}"
  end
end
```

Now, let’s create objects using this class

```rb
p1 = Person.new
p2 = Person.new

p1.set_first_name('Bola')
p2.set_first_name('Ahmed')
p p1, p2

#<Person:0x00007f995a890e40 @first_name="Bola">
#<Person:0x00007f995a890e18 @first_name="Ahmed">

p1.set_last_name('Buari')
p2.set_last_name('Aro')
p p1, p2

#<Person:0x00007fcfde888e38 @first_name="Bola", @last_name="Buari">
#<Person:0x00007fcfde888e10 @first_name="Ahmed", @last_name="Aro">

p1.full_name
p2.full_name
p p1, p2

#<Person:0x00007fb8d908cde0 @first_name="Bola", @last_name="Buari", @full_name="Bola Buari">
#<Person:0x00007fb8d908cdb8 @first_name="Ahmed", @last_name="Aro", @full_name="Ahmed Aro">
```

With the above example, we can observe that the instance variables are only for the instance of the class and are different for different instance even though it’s from the same class. Also, another thing to observe here is that the values of the instance variables are not reported until the methods that are assigning them to a value is called.

### Constants

Constants start with an upper case letter A-Z, similar to local variables when the variable is called before been assigned a value, it raises an error.

```rb
p Name
# uninitialized constant Name (NameError)
```

The error is a bit different, indicating that it is an “uninitialized constant”. Constants are not supposed to be reassigned new values, although it’s possible to reassign new values in some cases, it, however, raises a warning.

```rb
Name = 'Bola' # Line 1
Name = 'Ahmed' # Line 2

# ruby:2: warning: already initialized constant Name
# ruby:1: warning: previous definition of Name was here

p Name
# "Ahmed"
```

We can see from the example above how `Name` constant is been reassigned a new value.

### Pseudo-variables as listed below can not be assigned as a variable.

- `self` represents the top-level object,
- `nil` represents an undefined value
- `true` represents the boolean `true`
- `false` represents the boolean `false`,
- `__FILE__` is a `String` that represents the name of the current source file, for example, if, this variable is run on a file named “test.rb” printing `__FILE__` will outputs `”test.rb”`. Below is an example of creating a file, saving a

```sh
# create a file named "test.rb"
touch test.rb
# save the varaible "__FILE__", with a method to print it's value
echo "puts __FILE__" >> test.rb
# running the file outputs the following
ruby test.rb
"test.rb"
#
```

- `__LINE__` is an `Integer` that represents the current line number that variable is called. Continuing with the example below, we can add a line to the file `“puts __LINE__"`, this will print the Integer `2` since `“puts __LINE__"` would be at the second line to the file, to confirm this, we can also print the content of the file with `cat`. See example below:

```sh
# save the variable "__LINE__", with a method to print it's value
echo "puts __LINE__" >> test.rb
# running the file outputs the following
ruby test.rb
test.rb
2
# Outputs 2 as expected since the variable is called on the second line. We can see this by printing the content of the file as follows:
cat test.rb
puts __FILE__
puts __LINE__
```
