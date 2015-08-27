---
layout: post
title: "Microsoft did one thing right, C# (Part 1)"
---

## C# is an awesome language

###Here are some of my favorite features

#### The Using Statement

''' 
using(OracleConnection connect = new OracleConnection([Insert Connection string here]))
{
 // Here I'm going to use the connection somehow	
}
'''

The using statement essentially gets translated into a try/catch block, so this syntax
tells the garbage collector to avoid disposing the object while it's in the scope of the 
using statement. Remember, in order to use the using statement on an object you created, you need
to create an object that implements IDisposable

####LINQ

'''
	
	List<People> Students = new list<Student>();

	[Adding all the students here]

	//List for students with a GPA above 3.0
	List<Student> MagnaCumLaude = Student.Where(x => x.GPA > 3.0).ToList<Student>();

'''

Linq has a great, intuitive syntax. It works on anything that implements the interface IEnumerable and our good friend google can show you all the classes that implement IEnumerable

####Entity Framework

'''

	public class Student
	{
		#region Properties
		public double GPA{get; private set;}

		public string Name{get; set;}
		#endregion

		#region Constructors

		public Student(string Name = string.Empty, GPA = 0.0)
		{
			this.Name = (string.IsNullOrEmpty(Name))? "Jane Doe": Name;

			this.GPA = GPA
		}

		#endregion

	}
	//After the model is created
	public class ApplicationContext: DBContext
	{
		public ApplicationContext():base("DefaultConnection"){}

		public DBSet<Student> Students{get; set;}
	}

	//Now using it in a class

	public class schoolController{
		private ApplicationContext db = new ApplicationContext();

		public void AddStudent(String Name, double GPA)
		{
			//this adds a student to the Database
			db.Students.Add(new Student(Name, GPA));
		}
		public void GetGoodStudents(double standards)
		{
			return (from Student
				in db.Students
				where Student.GPA > standards
				select Student).ToList();
		}
	}

'''

The Entity Framework is an Object Relational Mapper that maps objects you created to a row in a database, but it has a couple of notable features

1.It could be code first, database first or some sort of combination in between.
2.You don't have to write 1x10^20 lines of code to pull, and create objects that encapsulate your data
3. It makes sense

#### MVVM with WPF

First let's say you have a grid in your XAML that formats the way the program will look

'''

	<grid>
	<button
	 Command = "{Binding NameCommand}"/>
	</grid>

'''

Then in the back-end, somewhere

'''

	Public ICommand NameCommand {get; set;}

'''

Then define a function that determines when the button should be enabled, this is Optional.

'''

	private bool CanName()
	{
		if(some property)
	      return true;
		return false;
	}

'''

This is what it will do

'''

	private void Name()
	{
		//Doing Something
	}

'''

and don't forget in your constructor

'''

	NameCommand = new RelayCommand(this.DoSomething, this.Name );

'''

Disclaimer: RelayCommand is a class inside of MVVM light, if you haven't referenced the framework, make sure to type


'''
	
	Install-Package MvvmLight

'''

###Key Notes


The MVVM design pattern was designed with the upmost modularity in mind. The View contains the format for the way the application should look. The ViewModel contains the business logic ( also referred to as the Controller
in MVC ) and the Model contains the objects that you've created and are using. For more information [MSDN Article](https://msdn.microsoft.com/en-us/magazine/Dn605875.aspx)

#####I love the MVVM Design pattern

MVVM is not perfect, it has a bit of an overhead, but it's a good separation of design goals.

Data-Binding is intuitive
