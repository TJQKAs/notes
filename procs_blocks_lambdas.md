####Bocks & Procs & Lambdas

#####Blocks

```
  array = [1, 2, 3, 4]

  array.collect! do |n|
  n ** 2
  end

  puts array.inspect

  => [1, 4, 9, 16]
  ```
1. First, we send the collect! method to an Array with a block of code.
2. The code block interacts with a variable used within the collect! method (n in this case) and squares it.
3. Each element inside the array is now squared.
