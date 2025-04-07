---
weight: 1
title: "Pro C# 10 with .NET 6 by Andrew Troelsen"
description: "Foundational Principles and Practices in Programming"
icon: "article"
date: "2025-04-05"
lastmod: "2025-04-06"
draft: false
toc: true
---
	Author: Johnny To
	Publish Date: 2025-04-05
	Last Modified: 2025-04-06

# Chapter 1 Notes

## Managed vs Unmanaged code
- Managed code - term used to describe the code targeting the .NET runtime.
- Assembly - a binary unit that contains the managed code.
- Unmanaged code - Code that cannot be directly hosted by the .NET runtime.
	- Can still be accessed from a C# program, but it locks you into a specific development and deployment target.

## Other .NET-Aware Programming Languages
- Visual Basic
- F#

## Overview of .NET Assemblies
- .NET Binaries take the same file extension as unmanaged Windows binaries ```(*.dll)``` while having no internal similarities.
	- .NET Binaries contain platform-agnostic Intermediate Language (IL) and type metadata.
- ```*.dll``` files created using a .NET compiler, the binary blob is termed an assembly.
	- 4 Basic Properties of this file
		- .NET Projects are always compiled to a file with a .dll extension even if the project is an executable.
			- Even if the project is an executable, can still be executed with the command ```dotnet <assembly name>.dll```
			- The ```dotnet.exe``` is actually copied to the build directory and renamed ```<assembly name>.exe``` which will then
			execute ```dotnet <assembly name>.dll```.
			- The ```*.exe``` is not even the actual project's code, just a convenient shortcut to running your application.
			- Even if the application is a single file that is executed directly. It's only a packaging convenience.
			It contains all the files needed to run the application and sometimes the .NET runtime included. However,
			the code is still running in a managed container just as if it were published as multiple files.
		- Assembly contains CIL (Common Intermediate Language) code.
		- Assembly contains metadata that describes in detail the characteristics of every ```type``` within the binary.
		- Contains a ```manifest``` that has information about the current version of the assembly, culture information, and a list of all externally
		referenced assemblies that are required for proper execution.


### Common Intermediate Language (CIL)
- Sits above any particular platform-specific instruction set.
- C# compiler emits CIL, not platform specific instructions.
	- For example, if you have a Calc.cs (Calculator class) that is compiled.
	It would produce a ```.dll``` assembly that contains a manifest, CIL instructions and metadata describing each aspect of the Calc and Program classes.
- Can output IL (Intermediate Language) of an assembly using ```ildasm.exe```.
- Doesn't matter if C# or Visual Basic or F#. You will find similar instructions when examining the CIL.
- Benefit is that it allows language integration.

### CIL to Platform-Specific Instructions
- Done by being compiled on the fly by a JIT compiler (also named jitter).
- The .NET runtime environment leverages a JIT compiler for each CPU targeting the runtime, each optimized for the underlying platform.
- A single body of code can be efficiently JIT compiled and executed on machines with different architectures.
- Jitter has a built in cache to avoid recompiling CIL. For example, if a method was compiled and ran once, then was needed to run again.
- Can pre-JIT code using ```crossgen.exe```.

### .NET Type Metadata
- Job of the compiler to generate the assembly's metadata.
- Describes every type (e.g. class, structure, enumeration) defined in the binary and the members of each type (e.g. properties, methods, and events).
- IntelliSense feature in Visual Studio is only possible by reading an assembly's metadata at design time.
- Also, it is used by various object-browsing utilities, debugging tools, and the C# compiler itself.
- It is the backbone of numerous .NET technologies including reflection, late beinding and object serialization.

### Assembly Manifest
- Metadata that describes the assembly itself.
- Documents all external assemblies required by the current assembly to function correctly.
	- The assembly's version number, copyright information, etc.
- The job of the compiler to generate the assembly's manifest.

## Common Type System (CTS)
- ```Type``` refers to a member of the set {```class```, ```interface```, ```structure```, ```enumeration```, ```delegate```}.
- Example:
	- You have a ```class``` that implements a number of ```interfaces``` where an interface method takes an ```enumeration type``` as a ```parameter``` and returns a ```structure```
	to the caller.
- However, only individuals who are deeply concerned with the inner workings of the CTS are those building tools and/or compilers that target the .NET platform.
- .NET Programmers need to learn how to work with the five types defined by the CTS in their language of choice.

### CTS Class Type
- Cornerstone of ```object-oriented programming (OOP)```.
- May be composed of an number of members such as
	- ```Constructors```
	- ```Properties```
	- ```Methods```
	- ```Events```
- In C#, classes are declared using the ```class``` keyword such as
``` csharp
// A C# class type with 1 method.
class Calc
{
	public int Add(int addend1, int addend2)
	{
		return addend1 + addend2;
	}
}
```

- CTS Class Characteristics
	- Is the class ```sealed```?
		- ```Sealed classes``` cannot function as a base class to other classes.
	- Does the class implement any ```interfaces```?
		- An ```interface``` is a collection of abstract members that provides a contract between the object and object user.
		- CTS allows a class to implement any number of interfaces.
	- Is the class ```abstract``` or ```concrete```?
		- ```Abstract classes``` cannot be directly instantiated but are intended to define common behaviors for derived types.
		- ```Concrete classes``` can be instantiated directly.
	- What is the ```visibility``` of this class?
		- Must be configured with a ```visibility``` keyword such as ```public``` or ```internal```.
		- Controls whether the class may be used by external assemblies or only from within the defining assembly.

### CTS Interface Type
- A named collection of abstract member definitions and/or default implementations which are implemented by a given class or structure.
- Defined using the ```interface``` keyword.
- By convention, all .NET interfaces begin with the capital letter ```I``` such as
``` csharp
// Usually decalred as public to allow types in other assemblies to implement their behavior.
public interface IDraw
{
	void Draw();
}
```
- On their own, interfaces have little use.
- When a class or structureimplements a given interface in its unique way, you are able to request access to the supplied functionality
- using an interface reference in a polymorphic manner.

### CTS Structure Type
- A lightweight class type having value-based semantics.
- Structures are best suited for modeling geometric and mathematical data.
- Created using the ```struct``` keyword such as
``` csharp
// A C# structure type.
struct Point
{
	// Structures can contain fields.
	public int xPos, yPos;

	// Structures can contain parameterized constructors.
	public Point (int x, int y)
	{ xPos = x; yPos = y;}

	// Strutures may define methods.
	public void PrintPosition()
	{
		Console.WriteLine("({0}, {1})", xPos, yPos);
	}
}
```

### CTS Enumeration Type
- Allows you to group name-value pairs.
- Example, if you were creating a video game application that allows the player to select from three character categories (Wizard, Fighter, or Thief).
- Rather than using numerical values to represent each possibility, you could build a strongly typed enumeration using the ```enum``` keyword.

``` csharp
enum CharacterTypeEnum
{
	Wizard = 100,
	Fighter = 200,
	Thief = 300
}
```

- By default, the storage used to hold each item is a 32-bit integer. Can be altered if needed.

### CTS Delegate Types
- .NET equivalent of a type-safe, C-style function pointer.
- .NET delegate is a class that derives from ```System.MulticastDelegate```, rather than a simple pointer to a raw memory address.
- Declared using the ```delegate``` keyword.

``` chsarp
//This C# delegate type can "point to" any method returning an int and taking two ints as input.
delegate int BinaryOp(int x, int y);
```

- Critical when you want to provide a way for one object to forward a call to another object and provide the foundation for the .NET event architecture.

### CTS Type Members
- Most ```types``` take any number of ```members```.
- A type member is constrained the the set
{```constructor```, ```finalizer```, ```static constructor```, ```nested type```, ```operator```, 
```method```, ```property```, ```indexer```, ```field```, ```readonly-field```, ```constant```, ```event```}
- CTS defines ```adornments``` that may be associated with a given member such as
	- Given a ```Visibility trait``` - public, private, protected.
	- Declared as ```abstract``` or ```virtual```
		- ```abstract``` - to enforce a polymorphic behavior on derived types.
		- ```virtual``` - to define a canned, but overridable, implementation.
	- Configured as ```static``` or ```instance```.
		- ```static``` - bound at the class level.
		- ```instance``` - bound at the object level.

### Intrinsic CTS Data Types
- Well-defined set of fundamental data types.
- All .NET language keywords resolve to the same CTS type defined in an assembly named ```mscorlib.dll```.
``` chsarp
CTS Data Type			C# Keyword
------------------------------------------
System.Byte				byte
System.SByte			sbyte
System.Int16			short
System.Int32			int
System.Int64			long
System.UInt16			ushort
System.UInt32			uint
System.UInt64			ulong
System.Single			float
System.Double			double
System.Object			object
System.Char				char
System.String			string
System.Decimal			decimal
System.Boolean			bool
```

- Unique keywords of a managed language are simply shorthand notations for a real type in the ```System``` namespace.
- For example the following code snippet defines a 32-bit numerical variable in C#.
``` csharp
// Define some "ints" in C#.
int i = 0;
System.Int32 j = 0;
```

## Common Language Specification (CLS)
- The CLS is a set of rules that describe in vivid detail the minimal and complet eset of features of a given .NET compiler must support to produce code that can be hosted by the
.NET Runtime, while at the same time be accessed in a uniform manner by all languages that target the .NET platform.
- CLS can be viewed as a subset of the full functionality defined by the CTS.
- The CLS is ultimately a set of rules that compiler builders must conform to if they intend their products to function seamlessly within the .NET universe.
- Each rule is defined a simple name (e.g. CLS Rule 6) and describes how this rule affects those who build compilers as well as those who interact with them.
- C# does define a number of programming constructs that are not CLS compliant.
	- You can instruct the C# compiler to check your code for CLS compliance using a single .NET attribute.
``` csharp
// Tell the C# compiler to check for CLS compliance.
[assembly: CLSCompliant(true)]
```
- This instructs the C# compiler to check every line of code against the rules of the CLS. If violations are discovered, you receive a compiler warning and a description of the offending code.

## .NET Runtime
- A collection of services that are required to execute a given compiled unit of code.
- .NET runtime provides a single, well-defined runtime layer that is shared by all languages and platforms that are .NET.

## Assembly vs Namespace vs Type
- Framework libraries is to give developers a well-defined set of existing code to leverage in their applications.
- .NET Libraries are language-neutral.
- Namespace keeps all the types within the base class libraries well organized.
- A namespace is a grouping of semantically related types in an assembly or possibly spread across multiple related assemblies.
- A single assembly can contain any number of namespaces, each of which can contain any number of types.
- Any language targeting the .NET runtime uses the same namespaces and the same types.
- 


- A convenient way to logically understand and organize related types.
- For example:
	- ```System``` namespace
		- ```System.Console``` from our perspective represents a class named ```Console``` that is contained within a namespace called System.
		- However, .NET runtime only sees it as a single class named ```System.Console```.
- The ```using``` keyword simplifies the process of referencing types defined in a particular namespace.
``` csharp
using System;

// The above statement enables the line of code below.
Console.WriteLine("10 + 84 is {0}", answer");

// Otherwise, the code would have been written as.
System.Console.WriteLine("10 + 84 is {0}", answer");
```


## Chapter 1 Vocabulary
-
