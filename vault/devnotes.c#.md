---
id: 30me5ye70hp7yvxy5rbc2kt
title: C#
desc: General C# Notes
updated: 1648058105831
created: 1648058105832
---
## General Info

## Try/Catch Exceptions

```csharp
        static void Main(string[] args)
        {
            string input = Console.ReadLine();
            try
            {
                int parsedInput = int.Parse(input);
                Console.WriteLine(parsedInput * 2);
            }
            catch (FormatException)
            {
                Console.WriteLine("Format exception please enter the correct type");
            }
            catch(OverflowException)
            {
                Console.WriteLine("Overflow Exception!");
            }
            catch(Exception)
            {
                Console.WriteLine("I dont know all the exceptions");
            }
```

## Unary Operators

`num2 = -num3` negative operator

`!` logical negation operator

## Increment Operators

`num++` or `++num`

## TryParse

```csharp
string numberAsString = "128"
int parsedValue
bool success = int.TryParse(numberAsString, out parsedValue);
if (success)
    Console.WriteLine("Parsing Successful - number is " + parsedValue);
else 
    Console.WriteLine("Parsing Failed");
```

## .Equals()

Determines whether two object instances are equal.

## Ternary Operator If Statements

```csharp
stateOfMatter = temp > 100 ? "gas" : temp < 0 ? "solid" : "liquid";
```
