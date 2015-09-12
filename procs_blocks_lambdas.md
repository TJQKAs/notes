####Bocks & Procs & Lambdas

#####Blocks

```
  array = [1, 2, 3, 4]  

  array.collect! do |n|                            ## for each element of our array we do n**2 statement
  n ** 2
  end

  puts array.inspect        ## method inspet returns a string containing a human-readable representation       

  => [1, 4, 9, 16]
  ```
1. First, we send the collect! method to an Array with a block of code.
2. The code block interacts with a variable used within the collect! method (n in this case) and squares it.
3. Each element inside the array is now squared.

If we want to make our own `collect!` method? We build a method called `iterate!` and see.
```
class Array                          
  def iterate!                                        ## create method iterate! with block 
    self.each_with_index do |n, i|                    ## to each of array elem i, we return "n"    
      self[i] = yield(n)                              ## yield(n) refers to method iterate! which makes 
    end                                               ## calculations
  end
end

array = [1, 2, 3, 4]

array.iterate! do |n|                               ## our method iterate!, where we square our elems of array 
  n ** 2                                            ## our calculations for "n" was sent  to "yield "(n)"
end

puts array.inspect

# => [1, 4, 9, 16]
```

1.  Send iterate! to the Array of numbers.
2.  When `yield` is called with the number `n` (first time is 1, second time is 2, etc…), pass the number to the block of code given.
3.  The block has the number available (also called `n`) and squares it. As it is the last value handled by the block, it is returned automatically.
4.  Yield outputs the value returned by the block, and rewrites the value in the array.
5.  This continues for each element in the array.

#####Procs 
```
class Array
  def iterate!(&code)      
    self.each_with_index do |n, i|
      self[i] = code.call(n)            ## instead of ' self[i] = yield(n) '
    end
  end
end

array = [1, 2, 3, 4]

array.iterate! do |n|
  n ** 2
end

puts array.inspect
```
The difference between blocks and Procs is that a block is a Proc that cannot be saved, and as such, is a one time use solution. Code which is reusable is called a Proc. Procs are objects, blocks are not. Proc is an instance of the Proc class.
```
class Array
  def iterate!(code)
    self.each_with_index do |n, i|
      self[i] = code.call(n)
    end
  end
end

array_1 = [1, 2, 3, 4]
array_2 = [2, 3, 4, 5]

square = Proc.new do |n|
  n ** 2
end

array_1.iterate!(square)
array_2.iterate!(square)

puts array_1.inspect
puts array_2.inspect
```
```
class Array
  def iterate!(code)                     ## 
    self.each_with_index do |n, i|       ## each elem i of array should get meaning n 
      self[i] = code.call(n)             ## 
    end
  end
end

def square(n)                          
  n ** 2
end

array = [1, 2, 3, 4]

array.iterate!(method(:square))          ## 1) take data from array  
                                         ## 2) take rules to what we should do with each elem from method iterate
puts array.inspect                       ## 3) calculate each elem by method square

# => [1, 4, 9, 16]
```
##### Differences Lambdas,Procs

1. Lambdas check the number of arguments, while procs do not
```
lam = lambda { |x| puts x }    # creates a lambda that takes 1 argument
lam.call(2)                    # prints out 2
lam.call                       # ArgumentError: wrong number of arguments (0 for 1)
lam.call(1,2,3)                # ArgumentError: wrong number of arguments (3 for 1)
```
Procs don’t care if they are passed the wrong number of arguments.

```
proc = Proc.new { |x| puts x } # creates a proc that takes 1 argument
proc.call(2)                   # prints out 2
proc.call                      # returns nil
proc.call(1,2,3)               # prints out 1 and forgets about the extra arguments
```

2. Lambdas and procs treat the `return` keyword differently `return` inside of a lambda triggers the code right outside of the lambda code
```
def lambda_test
  lam = lambda { return }
  lam.call
  puts "Hello world"
end

lambda_test                 # calling lambda_test prints 'Hello World'
```
‘return’ inside of a proc triggers the code outside of the method where the proc is being executed
```
def proc_test
  proc = Proc.new { return }
  proc.call
  puts "Hello world"
end

proc_test                 # calling proc_test prints nothing
```


based on http://www.reactive.io/tips/2008/12/21/understanding-ruby-blocks-procs-and-lambdas/


