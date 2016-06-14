# Typeclass polymorphism

In most object-oriented languages the unit of reuse is the object and by extension the class hierarchy. To reuse
existing logic in an object-oriented language users either subclass an existing class; override and introduce methods
to suit their needs or use methods on public interfaces as in the case of composition.

An example of a public interface for an animal within our zoo may be the following,

```
  trait Animal {
    def bname: (String, String)
  }
```

and a `Meerkat` would be defined something like,

```
  class Meerkat extends Animal {
    val bname: (String, String) = ("Suricata", "suricatta")
  }
```

It would then be possible to use the `Animal` interface to create methods which work on all subclasses of `Animal` provided
that the methods used were only on `Animal` such as a method to print the full name as a `String`

```
  def name(animal: Animal): String = s"${animal.bname._1}-${animal.bname._2}"
```

This starts to get tricky when we some more interfaces. Let's introduce the `Mammal` interface and the `Reptilian` interface, 
ignoring the platypus and echidna.

```
  trait Mammal {
    def furColours: Set[Colour]
  }
```

and,

```
  trait Reptile {
    def scaleColours: Set[Colour]
  }
```

Let's say I want to write a general method which takes in an `Animal` and returns something like,

```
  === Surica - suricatta ===
  furColour:      2
```


