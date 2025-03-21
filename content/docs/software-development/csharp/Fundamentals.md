﻿---
weight: 1
title: "Fundamentals"
description: ""
icon: "article"
date: "2025-03-08"
lastmod: "2025-03-09"
draft: false
toc: true
---
{{< alert context="info" 
	text="C# Language Quick References with definitions & examples." />}}

## Comments

```csharp
// Single line comment
/* Multi line comment */ 
```
## C# Project Structure
``` cpp
MyApp/                     // Root directory (Project folder)
	MyApp.sln              // Solution file (if using Visual Studio)
	MyApp.csproj           // Project file (contains dependencies, build info)
	Program.cs             // Entry point (contains Main method)
	Services/              // Folder for service-related classes
		DataService.cs     // Class for data-related operations
		EmailService.cs    // Class for email functionality
	Models/                // Folder for data models
		User.cs            // Class representing a user
		Product.cs         // Class representing a product
	Utilities/             // Folder for helper functions
		Logger.cs          // Class for logging functionality
	Properties/            // Auto-generated by Visual Studio (metadata, settings)
		AssemblyInfo.cs    // Assembly-level attributes

```
## Namespace & Classes
```csharp
// A namespace groups related code elements and prevents naming conflicts.
// It’s declared using the "namespace" keyword.

namespace School
{  
	class Student
	{
	
	}
	class Course
	{
	
	}
}
```

## Keywords & Their Usage

### Access Modifiers
```csharp
public       // Accessible anywhere
private      // Accessible only within the same class
protected    // Accessible within the same class and derived classes
internal     // Accessible within the same assembly
protected internal  // Combination of protected and internal
private protected  // Accessible within the same class and derived types in the same assembly
```

### Data Types
```csharp
int       // Integer
float     // Floating-point number
double    // Double precision floating-point number
decimal   // High-precision decimal number
char      // Single character
bool      // Boolean (true/false)
string    // String of characters
object    // Base type of all types
```

### Data Types
```csharp
if         // Conditional execution
else       // Executes if "if" condition is false
switch     // Multi-branch selection
case       // Defines case labels inside switch
default    // Default case in switch

for        // Traditional for loop
foreach    // Iterates over collections
while      // Loop with condition at the beginning
do         // Loop with condition at the end
break      // Exits the loop or switch statement
continue   // Skips current iteration in a loop
return     // Exits a function and returns a value
yield      // Returns an iterator element
```

### Control Flow
```csharp
try         // Defines a block to test for errors
catch       // Handles exceptions
finally     // Executes after try/catch, regardless of exceptions
throw       // Throws an exception
```

### Object-Oriented Programming (OOP)

```csharp
class       // Defines a class
struct      // Defines a struct (value type)
interface   // Defines an interface
enum        // Defines an enumeration
new         // Creates an object or calls a constructor
this        // Refers to the current instance of the class
base        // Refers to the base class constructor or members
namespace   // Defines a scope for related classes
using       // Imports a namespace or manages resources
abstract    // Defines an abstract class (cannot be instantiated)
sealed      // Prevents class inheritance
static      // Defines a static class/member
virtual     // Allows method overriding
override    // Overrides a virtual method in a derived class
readonly    // Makes a field immutable after initialization
const       // Declares a compile-time constant
```

### Multithreading & Asynchronous Programming
```csharp
async       // Marks a method as asynchronous
await       // Waits for an asynchronous operation
lock        // Prevents multiple threads from accessing a section
volatile    // Ensures a field is always read from memory, not cache
```

### Memory Management & Unsafe Code
``` csharp
unsafe      // Enables unsafe context (pointer operations)
fixed       // Prevents garbage collection from moving objects
stackalloc  // Allocates memory on the stack
sizeof      // Gets the size of a value type
typeof      // Gets the type metadata of a type
checked     // Enables overflow checking for numeric operations
unchecked   // Disables overflow checking
```

### Contextual Keywords
```csharp
var        // Implicitly typed variable
dynamic    // Allows runtime type changes
get        // Property getter
set        // Property setter
value      // Represents the assigned value in a property
nameof     // Gets the name of a variable, type, or member
is         // Checks if an object is a certain type
as         // Attempts to cast an object, returns null if failed
record     // Defines a record type (introduced in C# 9)
```

### Other Special Keywords
```csharp
default     // Gets the default value of a type
delegate    // Defines a method pointer type
event       // Declares an event
goto        // Jumps to a labeled statement (not recommended)
extern      // Declares an external method (e.g., for interoperability)
params      // Allows passing variable arguments to a method
partial     // Splits class definitions across multiple files
```