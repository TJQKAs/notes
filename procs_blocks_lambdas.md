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
  def iterate!                                        ## create method iterate! which uses
    self.each_with_index do |n, i|                    ## itself to each of array elem
      self[i] = yield(n)
    end
  end
end

array = [1, 2, 3, 4]

array.iterate! do |n|
  n ** 2
end

puts array.inspect

# => [1, 4, 9, 16]
```

1.  Send iterate! to the Array of numbers.
2.  When `yield` is called with the number `n` (first time is 1, second time is 2, etc…), pass the number to the block of code given.
3.  The block has the number available (also called `n`) and squares it. As it is the last value handled by the block, it is returned automatically.
4.  Yield outputs the value returned by the block, and rewrites the value in the array.
5.  This continues for each element in the array.






