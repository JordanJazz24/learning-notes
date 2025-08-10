La diferencia entre Console.Write y Console.WriteLine
Las tres nuevas líneas de código que agregó demostraron la diferencia entre los Console.WriteLine() métodos y Console.Write .

Console.WriteLine() imprime un mensaje en la consola de salida. Al final de la línea, agrega un avance de línea, como cuando se crea una línea de texto con la tecla Entrar o Retroceso del teclado.

Para imprimir en la consola de salida, pero sin agregar un avance de línea al final, ha utilizado la segunda técnica, Console.Write(). Por lo tanto, la siguiente llamada a Console.Write() imprime otro mensaje en la misma línea.

Los nombres de variable distinguen mayúsculas de minúsculas, lo que significa que string Value; y string value; son dos variables diferente

La var palabra clave indica al compilador de C# que el tipo de datos está implícito en el valor asignado. Una vez implícito el tipo, la variable actúa igual que si se hubiera usado el tipo de datos real para declararlo. La var palabra clave se usa para ahorrar pulsaciones de tecla cuando los tipos son largos o cuando el tipo es obvio por el contexto.
Las variables que usan la var palabra clave deben inicializarse.


Secuencias de escape de caracteres
Una secuencia de caracteres de escape es una instrucción para el entorno de tiempo de ejecución para que inserte un carácter especial que afectará a la salida de la cadena. 

Verbatim string literal
A verbatim string literal will keep all whitespace and characters without the need to escape the backslash. To create a verbatim string, use the @ directive before the literal string.


Console.WriteLine(@"    c:\source\repos    
        (this is where your code goes)");

Here's what you've learned about formatting literal strings so far:

Use character escape sequences when you need to insert a special character into a literal string, like a tab \t, new line \n, or a double quotation mark \".
Use an escape character for the backslash \\ when you need to use a backslash in all other scenarios.
Use the @ directive to create a verbatim string literal that keeps all whitespace formatting and backslash characters in a string.
Use the \u plus a four-character code to represent Unicode characters (UTF-16) in a string.
Unicode characters may not print correctly depending on the application.

string interpolation?
String interpolation combines multiple values into a single literal string by using a "template" and one or more interpolation expressions. An interpolation expression is indicated by an opening and closing curly brace symbol { }. You can put any C# expression that returns a value inside the braces. The literal string becomes a template when it's prefixed by the $ character.


You can combine string interpolation and verbatim literals by combining the symbols for each and using that as a prefix for the string template.



To see division working properly, you need to use a data type that supports fractional digits after the decimal point like decimal.

Order of operations
As you learned in the previous exercise, you can use the () symbols as the order of operations operators. However, this isn't the only way the order of operations is determined.

In math, PEMDAS is an acronym that helps students remember the order of operations. The order is:

Parentheses (whatever is inside the parenthesis is performed first)
Exponents
Multiplication and Division (from left to right)
Addition and Subtraction (from left to right)

----Call methods from the .NET Class Library using C#----

The .NET SDK and .NET Runtime
.NET is a cross-platform, open-source developer platform that's used to develop different types of applications. It includes the software languages and code libraries used to develop .NET applications. You can write .NET applications in C#, F#, or Visual Basic. The .NET platform is used to develop and run applications on Windows, macOS, and Linux. The .NET platform provides a runtime environment for running applications.

The .NET runtime is the code library that's required to run your C# applications. You may also see the .NET runtime referred to as the Common Language Runtime, or CLR. The .NET runtime isn't required to write your C# code, but it's required to actually run your C# applications.

Visual Studio Code uses the .NET SDK and C# extensions to provide a development environment for writing, running, and debugging C# applications.



The .NET Class Library is a collection of thousands of classes containing tens of thousands of methods. For example, the .NET Class Library includes the Console class for developers working on console applications. The Console class includes methods for input and output operations such as Write(), WriteLine(), Read(), ReadLine(), and many others.


Some methods don't rely on the current state of the application to work properly. In other words, stateless methods are implemented so that they can work without referencing or changing any values already stored in memory. Stateless methods are also known as static methods.

For example, the Console.WriteLine() method doesn't rely on any values stored in memory. It performs its function and finishes without impacting the state of the application in any way.


Other methods, however, must have access to the state of the application to work properly. In other words, stateful methods are built in such a way that they rely on values stored in memory by previous lines of code that have already been executed. Or they modify the state of the application by updating values or storing new values in memory. They're also known as instance methods.



The new operator does several important things:

It first requests an address in the computer's memory large enough to store a new object based on the Random class.
It creates the new object, and stores it at the memory address.
It returns the memory address so that it can be saved in the dice object.






Oftentimes, the terms 'parameter' and 'argument' are used interchangeably. However, 'parameter' refers to the variable that's being used inside the method. An 'argument' is the value that's passed when the method is called.

Overloaded methods support several implementations of the method, each with a unique method signature (the number of parameters and the data type of each parameter).

--Add decision logic to your code using `if`, `else`, and `else if` statements in C#---



A Boolean expression is any code that returns a Boolean value, either true or false. The simplest Boolean expressions are simply the values true and false. Alternatively, a Boolean expression could be the result of a method that returns the value true or false



A code block is a collection of one or more lines of code that are defined by an opening and closing curly brace symbol { }.



Here you combine three Boolean expressions to create one composite Boolean expression in a single line of code. This is sometimes called a compound condition. You have one outer set of parentheses that combines three inner sets of parentheses separated by two pipe characters.


--Store and iterate through sequences of data using Arrays and the foreach statement in C# --


An array is a collection of individual data elements accessible through a single variable name. You use a zero-based numeric index to access each element of an array. Arrays allow you to create a collection of data values that shares a common purpose or characteristics under a single variable name for easier processing.

Notice that the first set of square brackets [] merely tells the compiler that the variable named fraudulentOrderIDs is an array, but the second set of square brackets [3] indicates the number of elements that the array can hold.

The foreach statement provides a simple, clean way to iterate through the elements of an array. The foreach statement processes array elements in increasing index order, starting with index 0 and ending with index Length - 1. It uses a temporary variable to hold the value of the array element associated with the current iteration. Each iteration will run the code block that's located below the foreach declaration.

The foreach statement sets the value of the current element in the array to a temporary variable, which you can use in the body of the code block.



---Create readable code with conventions, whitespace, and comments in C#--



Variable names can contain alphanumeric characters and the underscore (_) character. Special characters like the pound #, the dash -, and the dollar sign $ are not allowed.
Variable names must begin with an alphabetical letter or an underscore, not a number. Using an underscore character to start a variable name is typically reserved for private instance fields. A link to further reading can be found in the module summary.
Variable names must NOT be a C# keyword. For example, these variable name declarations won't be allowed: float float; or string string;.
Variable names are case-sensitive, meaning that string MyValue; and string myValue; are two different variables.



Use code comments to leave meaningful notes to yourself about the problem your code solves.



-----------------------

What is the conditional operator?
The conditional operator ?: evaluates a Boolean expression and returns one of two results depending on whether the Boolean expression evaluates to true or false. The conditional operator is commonly referred to as the ternary conditional operator.


----
For the first code sample, the compiler interprets flag as a Boolean variable that could be assigned a value of either true or false. The compiler concludes that if flag is false, value will not be initialized when the second Console.WriteLine() is executed. Essentially the compiler considers the following two code execution paths to be possible:

When implementing an if statement that includes a single-statement code block, Microsoft recommends that you consider these conventions:

Never use single-line form (for example: if (flag) Console.WriteLine(flag);
Using braces is always accepted, and required if any block of an if/else if/.../else compound statement uses braces or if a single statement body spans multiple lines.
Braces may be omitted only if the body of every block associated with an if/else if/.../else compound statement is placed on a single line.



