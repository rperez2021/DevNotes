---
id: jyynuo7mhr9otadkfmgqydu
title: Type Conversion
desc: Notes on Type Conversion and Type Casting
updated: 1647291487227
created: 1647290696344
---
## General Info

[Microsoft Docs Reference](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/casting-and-type-conversions)

### Implicit Conversions

When no special syntax is required because the conversion always succeeds. For example conversions from a small integral type (ex `int`) to a larger one (ex `long`)

### Casting (Explicit Conversions)

Casting is required when information might be lost in the conversion, or when the conversion might not succeed for other reasons. Typical examples include numeric conversion to a type that has less precision or a smaller range, and conversion of a base-class instance to a derived class.

```csharp
double myDouble = 13.37;
int myInt;

//cast double to int
myInt = (int)myDouble;
```

### User-Defined Conversions

User-defined conversions are performed by special methods that you can define to enable explicit and implicit conversions between custom types that do not have a base class–derived class relationship.

### Conversions with Helper Classes

Such as using `.ToBoolean()` or `.ToString()` or `.ToChar()`
