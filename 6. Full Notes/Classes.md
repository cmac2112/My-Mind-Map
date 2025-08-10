
2025-08-10 18:22

Status:

Tags: [[Object Oriented]], [[C(SHARP)]], [[Java]], [[JavaScript]], [[Typescript]], [[Python]]

# Classes

A class is an abstract blueprint that creates more specific concrete objects. Classes often represent broad categories like Car or Dog, that share attributes. These classes define what attributes and instance of this type will have, like color, but not the value of those attributes for a specific object.

[[Objects]] in this case are an instance of a class, When a class is defined, no memory is allocation, but when it is [[Instantiated]] memory is allocated.

### c\# class
```

public class Dog{
	public int Age {get; set;}
	public string Name {get; set;}
	public Breed DogBreed {get; set;}
}
```

classes can use other defined types than just primitive types. In the case of `Breed`

```
public class Breed{
	public string Name {get; set;}
	public string Color {get; set;}
	etc...
}
```

This works well for [[ORMs]] such as [[EFCore]] which will allow you to query tables and return them as objects in themselves.

