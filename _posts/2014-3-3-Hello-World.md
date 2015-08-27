---
layout: post
title: "Microsoft did one thing right, C#"
---

## C# is an awesome language

###Here are some of my favorite features

#### The Using Statement

> using(OracleConnection connect = new OracleConnection(<connectionString>))
> {
> // Here I'm going to use the connection somehow	
>}

The using statement essentially gets translated into a try/catch block, but this 
syntax allows for simplicity and a greater ability to express yourself with code.

#### MVVM with WPF

First let's say you have a grid in your XAML that formats the way the program will look

><grid>
><button
> Command = "{Binding Command Name}"/>
></grid>

Then in the back-end

>Public ICommand Name{get; set;}

Then define your function

This is Optional
>private bool CanName()
>{
>	if(some property)
>      return true;
>	return false;
>}

This is what it will do

>private void DoSomething()
>{
>	//Doing Something
>}

#####I love the MVVM Design pattern

MVVM is not perfect, it has a bit of an overhead, but it's a good separation of design goals.

Data-Binding is intuitive
