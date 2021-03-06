---
title: Switch Case
---

# Switch Case

Switch is a selection statement that chooses a switch case section depending on the value matched with the expression/value being evaluated.<sup>1</sup>  If none of the case statements match the value of the switched variable, the default path is chosen. The switch statement is like a set of `if statements`. We exit from the switch by `break`.

## Example
```
public enum Colors { Red, Blue, Green, Orange }

Colors myColor;

... myColor is set to one of the enum values ...

switch(myColor){
  case Colors.Red: 
    Console.WriteLine("How you like them apples?");
    break;
  case Colors.Blue: 
    Console.WriteLine("Ice Ice Baby...");
    break;
  case Colors.Green: 
    Console.WriteLine("Fore!");
    break;
  default:
    Console.WriteLine("I have a hard time when I try to rhyme.");
}
```

## Output
```
If myColor is Colors.Red:
> How you like them apples?

If myColor is Colors.Blue:
> Ice Ice Baby...

If myColor is Colors.Green:
> Fore!

If myColor is Colors.Orange:
> I have a hard time when I try to rhyme.

```

## Fallthrough

It is also possible to use multiple statements produce the same outcome, by letting the cases 'fallthrough', like so:

```
switch(myColor) {
  case Colors.Red:
  case Colors.Blue:
    //Code
    break;
  ...
 }
```
This will execute the same lines of code if myColor is either Red or Blue.

## When clause

Starting with C# 7.0 you can use `when` clause to specify additional condition that must be satisfied. When clause is optional and is used right after specific case.

```csharp
Dog dog = new Dog
{
    Name = "Charlie",
    Breed = "Affenpinscher",
    Age = 3
};

switch (dog)
{
    case Dog d when d.Breed == "Affenpinscher" && d.Age >= 6:
        Console.WriteLine($"{dog.Name} is considered a senior dog.");
        break;
    case Dog d when d.Breed == "Affenpinscher" && d.Age >= 2:
        Console.WriteLine($"{dog.Name} is considered an adult dog.");
        break;
    case Dog d when d.Breed == "Affenpinscher":
        Console.WriteLine($"{dog.Name} is considered a puppy.");
        break;
    case Dog d when d.Breed == "Chihuahua" && d.Age >= 4:
        Console.WriteLine($"{dog.Name} is considered a senior dog.");
        break;
    case Dog d when d.Breed == "Chihuahua" && d.Age >= 2:
        Console.WriteLine($"{dog.Name} is considered an adult dog.");
        break;
    case Dog d when d.Breed == "Chihuahua":
        Console.WriteLine($"{dog.Name} is considered a puppy.");
        break;
    default:
        Console.WriteLine($"We have no information according {dog.Breed} breed.");
        break;
}
```
As you see in the above example after `when` keyword you should specify logical condition (an instruction that returns bool value).

## Pattern matching using switch case

We can use switch to not only match certain values, but also match certain data type. This is called pattern matching

## Example

Lets say that we have some different types of shapes:
```csharp
  public class Square
  {
      public double Side { get; }

      public Square(double side)
      {
          Side = side;
      }
  }
  
  public class Circle
  {
      public double Radius { get; }

      public Circle(double radius)
      {
          Radius = radius;
      }
  }
  
  public struct Rectangle
  {
      public double Length { get; }
      public double Height { get; }

      public Rectangle(double length, double height)
      {
          Length = length;
          Height = height;
      }
  }
```

And now we want to create a method which calculates area for any shape we pass to it. We can do that using pattern matching in switch statement like so:
```csharp
  public static double ComputeAreaModernSwitch(object shape)
  {
      switch (shape)
      {
          case Square s:
              return s.Side * s.Side;
          case Circle c:
              return c.Radius * c.Radius * Math.PI;
          case Rectangle r:
              return r.Height * r.Length;
          default:
              throw new ArgumentException(
                  message: "shape is not a recognized shape",
                  paramName: nameof(shape));
      }
  }
```

### Sources:
- 1 https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/switch
- https://docs.microsoft.com/en-us/dotnet/csharp/pattern-matching
