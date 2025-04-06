---
weight: 1
title: "Pro C# 10 with .NET 6 by Andrew Troelsen"
description: "Foundational Principles and Practices in Programming"
icon: "article"
date: "2025-04-05"
lastmod: "2025-04-05"
draft: false
toc: true
---
	Author: Johnny To
	Publish Date: 2025-04-05
	Last Modified: 2025-04-05

# Notes

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
		- Assembly contains CIL code.
		- Assembly contains metadata that describes in detail the characteristics of every ```type``` within the binary.
		- Contains a ```manifest``` that has information about the current version of the assembly, culture information, and a list of all externally
		referenced assemblies that are required for proper execution.


