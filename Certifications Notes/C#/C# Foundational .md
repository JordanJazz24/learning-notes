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









