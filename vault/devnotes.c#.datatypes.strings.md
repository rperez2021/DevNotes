---
id: vpx4bmx8pfcw9514uqqb7sw
title: Strings
desc: 'Notes on String DataType'
updated: 1647293115642
created: 1647291861826
---
## General Info

### Verbatim Strings

Using an @ sign in the beginning of a large string copy will maintain string formatting in the console it also prevents using escaped characters to work.

## Methods

### String Formatting

```csharp
string s = String.Format("The current price is {0} per ounce.", pricePerOunce);
```

### String Interpolation

```csharp
string name = "Horace";
int age = 34;
Console.WriteLine($"He asked, \"Is your name {name}?\", but didn't wait for a reply :-{{");
Console.WriteLine($"{name} is {age} year{(age == 1 ? "" : "s")} old.");
// Expected output is:
// He asked, "Is your name Horace?", but didn't wait for a reply :-{
// Horace is 34 years old.
```


### Substring

```csharp
string firstName = "Robert";
Console.WriteLine(firstName.Substring(2)); // will output bert
```

`.IsNullOrWhiteSpace()`.
