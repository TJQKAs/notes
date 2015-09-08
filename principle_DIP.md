#### There I describe shortly the The Dependency Inversion Principle - the one of the S.O.L.I.D principles.

The Dependency Inversion Principle has two parts:

###### * High-level modules should not depend on low-level modules. Both should depend on abstractions.
###### * Abstractions should not depend upon details. Details should depend upon abstractions.

Thus using this principle you may be able construct some programm with many classes, you can declare what this classes should do, but it doesn't mean that these classes fulfill somethings. In other words, in high level class you can only declare the interface of low-level class implying that it shoul do something, but it dosen't mean that it makes something, at least at the moment when you are presenting (showing) you program structure. 

#####Example:
```
 class Report
  def body
     generate_reporty_stuff
  end
  def print
     JSONFormatter.new.format(body)
  end
end
class JSONFormatter
  def format(body)
     ...
  end
end 
``` 
The Report class is hardcoded it by class Formatter, thus we see  a dependency from the Report to the JSONFormatter. Since the Report is a more abstract (high-level) concept than the JSONFormatter, we're effectively breaking the DIP.

We can solve it with dependency injection:
```
class Report
  def body
     generate_reporty_stuff
  end
  def print(formatter: JSONFormatter.new)
     formatter.format body
  end
end
```
In the second case we just imply that there is The class JSONFormatter, but it doesn't exist.

