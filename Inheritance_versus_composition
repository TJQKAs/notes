Describe the difference between composition and inheritance.

Inheritance is used is used when we want a new a class to inherit the features/methods from its parent class. The 'child' class will be able to use all features of its 'parent' class. However, any modifications made to the child class will only affect the child class, and not the parent which will remain as originally defined.

````

class Parent
   def override
      puts "Parent string"
   end
end

class Child < Parent
   def override
      puts "Child string"
   end
end

parent = Parent.new
child = Child.new

parent.override ===> "Parent string"
child.override ===> "Child string"

````

Composition on the other hand does not alter or even require a parent class. Composition is used so that our primary class works in harmony with a module (or class) that has methods which our primary class could access when it requires a different method. The code from the module is not overwriting anything within our primary class but rather the primary class is accessing the method from the module.  

What are some of the dangers of inheritance?

It can overwrite code in the subclass which you did not intend it to do so.

It can also make make your code overcomplicated and difficult when trying to try the heirarchy of your individual classes and their methods.

Why would we prefer composition over inheritance?

A major benefit of composition is that it adheres to the DRY principle. If we know that we are going to be using a method across many different classes then we can place that method in a module which we can access across all of our classes rather than defining it in each class.

When we use composition we are able to access specific methods that we require to suit the classes individual needs. Whereas if we were to inherit the classes we risk overriding methods in our child class that we did not wish to alter.

Give code examples of using inheritance to build ships.

Example: (some code removed for brevity)

`````

class Ship

  def initialize
    @number_of_hits = ['X', 'X'] ## This is how many lives the ship has/size of ship
  end

  def receive_hit
    # This method removes a live from our number_of_hits array
  end

end

class Aircraft_Carrier < Ship
   def initialize
     @number_of_hits = ['X', 'X', 'X', 'X', 'X']
   end
end

````
In this example our subclass Battleship inherits the method receive_hit from the parent class Ship. This is a method that all different types of ship would require. However, it alters the @number_of_hits array as each class of ship will have different lives according to its size.
