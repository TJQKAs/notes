## There I describe shortly the The Dependency Inversion Principle - the one of the S.O.L.I.D principles.

The Dependency Inversion Principle has two parts:
1)  High-level modules should not depend on low-level modules. Both should depend on abstractions.
2)  Abstractions should not depend upon details. Details should depend upon abstractions.
Rather than working with a set of classes that are hard wired (tightly coupled) to each other, you want to work with a standard interface. Furthermore, you want to ensure that you can replace the implementation without violating the expectations of that interface. So, if you’re working with an interface and you want to be able to replace it, then you need to ensure that you are only working with the interface and never with a concrete implementation. That is, the code that relies on the interface should only ever know about the interface. It should not know about any of the specific classes that implement the interface.
As an aside, in object oriented programming, an 'interface' generally defines the set of methods (or messages) that an instance of a class that has that interface could respond to. As a programmer, you will want to reduce direct coupling of classes whenever possible. You want to decouple your system so that you can change individual pieces without having to change anything more than the individual piece. The Dependency Inversion Principle is the key to this goal. By depending only on an abstraction such as an interface or base class, you can correct the coupling of the various parts of the system. This allows you to re-compose the system with different implementations.
EXAMPLE:
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
 In this case the JSONFormatter class has been hardcoded into the Report class, thus creating a dependency from the Report to the JSONFormatter. Since the Report is a more abstract (high-level) concept than the JSONFormatter, this is effectively breaking the DIP.
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
At the second case we see that we create an example of class JSONFormatter and put it as an argument of the method print. 
