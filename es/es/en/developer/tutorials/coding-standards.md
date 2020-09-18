---
title: Coding Standards
uid: en/developer/tutorials/coding-standards
author: git.AndreiMaz
contributors: git.DmitriyKulagin
---

# Estándares de codificación

Hay tres categorías de convenciones de codificación .NET compatibles:

## Convenciones de idioma

### Configuración de estilo de código .NET

#### "esta." calificadores

Esta regla de estilo se puede aplicar a campos, propiedades, métodos o eventos.

- Prefiere que el elemento de código *no* esté precedido por `this`.
- Prefiere que los campos *no* estén precedidos por `this.`

  ```csharp
  //Right
  capacity = 0;
  ```

  ```csharp
  //Wrong
  this.capacity = 0;
  ```

- Prefer properties *not* to be prefaced with `this.`

  ```csharp
  //Right
  ID = 0;
  ```

  ```csharp
  //Wrong
  this.ID = 0;
  ```

- Prefer methods *not* to be prefaced with `this.`

  ```csharp
  //Right
  Display();
  ```

  ```csharp
  //Wrong
  this.Display();
  ```

- Prefer events *not* to be prefaced with `this.`

  ```csharp
  //Right
  Elapsed += Handler;
  ```

  ```csharp
  //Wrong
  this.Elapsed += Handler;
  ```

#### Palabras clave de idioma en lugar de nombres de tipo de marco para referencias de tipo

Esta regla de estilo se puede aplicar a variables locales, parámetros de método y miembros de clase, o como una regla separada para escribir expresiones de acceso a miembros.

- Prefiera la palabra clave de idioma para variables locales, parámetros de método y miembros de clase, en lugar del nombre de tipo, para tipos que tienen una palabra clave para representarlos.

  ```csharp
  //Right
  private int _member;
  ```

  ```csharp
  //Wrong
  private Int32 _member;
  ```

- Prefiera la palabra clave del idioma para las expresiones de acceso a miembros, en lugar del nombre del tipo, para los tipos que tienen una palabra clave para representarlos.

  ```csharp
  //Right
  var local = int.MaxValue;
  ```

  ```csharp
  //Wrong
  var local = Int32.MaxValue;
  ```

#### Preferencias de modificadores

Las reglas de estilo de esta sección se refieren a las preferencias de los modificadores, incluido el requerimiento de modificadores de accesibilidad, la especificación del orden de clasificación del modificador deseado y el requerimiento del modificador de solo lectura.

- Prefiere que se declaren modificadores de accesibilidad, excepto para los miembros de la interfaz pública.

  ```csharp
  //Right
  class MyClass
  {
      private const string thisFieldIsConst = "constant";
  }
  ```

  ```csharp
  //Wrong
  class MyClass
  {
      const string thisFieldIsConst = "constant";
  }
  ```

- Prefer the specified ordering:

	*`public, private, protected, internal, static, extern, new, virtual, abstract, sealed, override, readonly, unsafe, volatile, async:silent`*

  ```csharp
  //Right
  class MyClass
  {
      private static readonly int _daysInYear = 365;
  }
  ```

#### Preferencias de paréntesis

Las reglas de estilo de esta sección se refieren a las preferencias de paréntesis, incluido el uso de paréntesis para operadores aritméticos, relacionales y otros operadores binarios.

- Preferir paréntesis para aclarar la precedencia del operador aritmético (*, /, %, +, -, <<, >>, &, ^, |)

  ```csharp
  //Right
  var v = a + (b * c);
  ```

  ```csharp
  //Wrong
  var v = a + b * c;
  ```

-Prefiere paréntesis para aclarar el operador relacional (>, <, <=, >=, is, as, ==, !=) es, como Precedencia

  ```csharp
  //Right
  var v = (a < b) == (c > d);
  ```

  ```csharp
  //Wrong
  var v = a < b == c > d;
  ```

- Prefiere los paréntesis para aclarar la precedencia de otros operadores binarios (&&, ||, ??)

  ```csharp
  //Right
  var v = a || (b && c);
  ```

  ```csharp
  //Wrong
  var v = a || b && c;
  ```

-Prefiero no tener paréntesis cuando la precedencia del operador es obvia

  ```csharp
  //Right
  var v = a.b.Length;
  ```

  ```csharp
  //Wrong
  var v = (a.b).Length;
  ```

#### Preferencias de nivel de expresión

Las reglas de estilo de esta sección se refieren a las preferencias de nivel de expresión, incluido el uso de inicializadores de objeto, inicializadores de colección, nombres de tuplas explícitos o inferidos y tipos anónimos inferidos.

- Prefiere que los objetos se inicialicen utilizando inicializadores de objetos cuando sea posible

  ```csharp
  //Right
  var c = new Customer() { Age = 21 };
  ```

  ```csharp
  //Wrong
  var c = new Customer();
  c.Age = 21;
  ```

- Prefiere que las colecciones se inicialicen usando inicializadores de colección cuando sea posible

  ```csharp
  //Right
  var list = new List<int> { 1, 2, 3 };
  ```

  ```csharp
  //Wrong
  var list = new List<int>();
  list.Add(1);
  list.Add(2);
  list.Add(3);
  ```

- Prefiere los nombres de tupla a las propiedades de ItemX

  ```csharp
  //Right
  (string name, int age) customer = GetCustomer();
  var name = customer.name;
  ```

  ```csharp
  //Wrong
  (string name, int age) customer = GetCustomer();
  var name = customer.Item1;
  ```

- Prefer inferred tuple element names

  ```csharp
  //Right
  var tuple = (age, name);
  ```

  ```csharp
  //Wrong
  var tuple = (age: age, name: name);
  ```

- Prefer explicit anonymous type member names

  ```csharp
  //Right
  var anon = new { age = age, name = name };
  ```

  ```csharp
  //Wrong
  var anon = new { age, name };
  ```

- Prefiere las propiedades automáticas a las propiedades con campos de respaldo privados

  ```csharp
  //Right
  private int Age { get; }
  ```

  ```csharp
  //Wrong
  private int age;

  public int Age
  {
      get
      {
          return age;
      }
  }
  ```

- Prefiero usar una verificación nula con coincidencia de patrones *`object.ReferenceEquals`*

  ```csharp
  //Right
  if (value is null)
      return;
  ```

  ```csharp
  //Wrong
  if (object.ReferenceEquals(value, null))
      return;
  ```

- Prefiere asignaciones con un condicional ternario sobre una instrucción if-else

  ```csharp
  //Right
  string s = expr ? "hello" : "world";
  ```

  ```csharp
  //Wrong
  string s;
  if (expr)
  {
      s = "hello";
  }
  else
  {
      s = "world";
  }
  ```

- Prefiere declaraciones de retorno para usar un condicional ternario sobre una instrucción if-else

  ```csharp
  //Right
  return expr ? "hello" : "world"
  ```

  ```csharp
  //Wrong
  if (expr)
  {
      return "hello";
  }
  else
  {
      return "world";
  }
  ```

- Prefiere expresiones de asignación compuestas

  ```csharp
  //Right
  x += 1;
  ```

  ```csharp
  //Wrong
  x = x + 1;
  ```

#### Preferencias de verificación nula

Las reglas de estilo de esta sección se refieren a las preferencias de verificación de nulos.

- Prefiere expresiones de fusión nula a la verificación de operadores ternarios

  ```csharp
  //Right
  var v = x ?? y;
  ```

  ```csharp
  //Wrong
  var v = x != null ? x : y; // or
  var v = x == null ? y : x;
  ```

- Prefiere usar un operador condicional nulo cuando sea posible

  ```csharp
  //Right
  var v = o?.ToString();
  ```

  ```csharp
  //Wrong
  var v = o == null ? null : o.ToString(); // or
  var v = o != null ? o.String() : null;
  ```

### Configuración de estilo de código C#

#### Tipos implícitos y explícitos

Las reglas de estilo en esta sección se refieren al uso de la palabra clave var frente a un tipo explícito en una declaración de variable. Esta regla se puede aplicar por separado a los tipos integrados, cuando el tipo es aparente y en otros lugares.

- Preferir *`var`* se usa para declarar variables con tipos de sistema integrados como *`int`*

  ```csharp
  //Right
  var x = 5;
  ```

  ```csharp
  //Wrong
  int x = 5;
  ```

-Prefiera *`var`* cuando el tipo ya se menciona en el lado derecho de una expresión de declaración

  ```csharp
  //Right
  var obj = new Customer();
  ```

  ```csharp
  //Wrong
  Customer obj = new Customer();
  ```

-Prefiere *`var`* sobre el tipo explícito en todos los casos, a menos que sea anulado por otra regla de estilo de código

  ```csharp
  //Right
  var f = this.Init();
  ```

  ```csharp
  //Wrong
  bool f = this.Init();
  ```

#### Miembros con cuerpo de expresión

Las reglas de estilo de esta sección se refieren al uso de [miembros con cuerpo de expresión](https://docs.microsoft.com/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members) cuando la lógica consta de una sola expresión. Esta regla se puede aplicar a métodos, constructores, operadores, propiedades, indexadores y descriptores de acceso.

- Prefer block bodies for methods

  ```csharp
  //Right
  public int GetAge() { return this.Age; }
  ```

  ```csharp
  //Wrong
  public int GetAge() => this.Age;
  ```

- Prefer block bodies for constructors

  ```csharp
  //Right
  public Customer(int age) { Age = age; }
  ```

  ```csharp
  //Wrong
  public Customer(int age) => Age = age;
  ```

- Prefer block bodies for operators

  ```csharp
  //Right
  public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
  { return new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary); }
  ```

  ```csharp
  //Wrong
  public static ComplexNumber operator + (ComplexNumber c1, ComplexNumber c2)
      => new ComplexNumber(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary);
  ```

- Prefiera cuerpos de expresión para propiedades cuando serán una sola línea

  ```csharp
  //Right
  public int Age => _age;
  ```

  ```csharp
  //Wrong
  public int Age { get { return _age; }}
  ```

- Preferir cuerpos de expresión para indexadores

  ```csharp
  //Right
  public T this[int i] => _values[i];
  ```

  ```csharp
  //Wrong
  public T this[int i] { get { return _values[i]; } }
  ```

- Prefer expression bodies for accessors

  ```csharp
  //Right
  public int Age { get => _age; set => _age = value; }
  ```

  ```csharp
  //Wrong
  public int Age { get { return _age; } set { _age = value; } }
  ```

- Prefer expression bodies for lambdas

  ```csharp
  //Right
  Func<int, int> square = x => x * x;
  ```

  ```csharp
  //Wrong
  Func<int, int> square = x => { return x * x; };
  ```

#### La coincidencia de patrones

Las reglas de estilo de esta sección se refieren al uso de [coincidencia de patrones](https://docs.microsoft.com/dotnet/csharp/pattern-matching) en C #.

- Prefiere la coincidencia de patrones en lugar de expresiones con conversiones de tipo

  ```csharp
  //Right
  if (o is int i) {...}
  ```

  ```csharp
  //Wrong
  if (o is int) {var i = (int)o; ... }
  ```

- Prefiere la coincidencia de patrones en lugar de expresiones *`as`* con comprobaciones nulas para determinar si algo es de un tipo en particular

  ```csharp
  //Right
  if (o is string s) {...}
  ```

  ```csharp
  //Wrong
  var s = o as string;
  if (s != null) {...}
  ```

#### Declaraciones de variables en línea

Esta regla de estilo se refiere a si las variables de salida se declaran en línea o no. A partir de C # 7, puede [declarar una variable de salida en la lista de argumentos de una llamada de método](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/out-parameter-modifier#calling- un-método-con-un-argumento-out), en lugar de en una declaración de variable separada.

- Prefiere que las variables *`out`* se declaren en línea en la lista de argumentos de una llamada al método cuando sea posible

  ```csharp
  //Right
  if (int.TryParse(value, out int i) {...}
  ```

  ```csharp
  //Wrong
  int i;
  if (int.TryParse(value, out i) {...}
  ```

#### Preferencias de nivel de expresión de C #

Esta regla de estilo se refiere al uso del [literal predeterminado para expresiones de valor predeterminado](https://docs.microsoft.com/dotnet/csharp/programming-guide/statements-expressions-operators/default-value-expressions#default-literal-and -type-inference) cuando el compilador puede inferir el tipo de expresión.

- Prefer *`default`* over *`default(T)`*

  ```csharp
  //Right
  void DoWork(CancellationToken cancellationToken = default) { ... }
  ```

  ```csharp
  //Wrong
  void DoWork(CancellationToken cancellationToken = default(CancellationToken)) {   ... }
  ```

#### Preferencias de comprobación de nulos de C #

Estas reglas de estilo se refieren a la sintaxis en torno a la verificación nula, incluido el uso de expresiones throw o declaraciones throw, y si realizar una verificación nula o utilizar el operador de fusión condicional (?.) Al invocar un [lambda expression](https://docs.microsoft.com/dotnet/csharp/lambda-expressions).

- Prefer to use throw expressions instead of throw statements

  ```csharp
  //Right
  this.s = s ?? throw new ArgumentNullException(nameof(s));
  ```

  ```csharp
  //Wrong
  if (s == null) { throw new ArgumentNullException(nameof(s)); }
  this.s = s;
  ```

- Consulte el uso del operador de fusión condicional (?.) Al invocar una expresión lambda, en lugar de realizar una comprobación nula

  ```csharp
  //Right
  func?.Invoke(args);
  ```

  ```csharp
  //Wrong
  if (func != null) { func(args); }
  ```

#### Preferencias de bloque de código

Esta regla de estilo se refiere al uso de llaves { } para rodear bloques de código.

- Prefiera no usar llaves si está permitido

  ```csharp
  //Right
  if (test) this.Display();
  ```

  ```csharp
  //Wrong
  if (test) { this.Display(); }
  ```

## Convenciones de formato

### Configuración de formato .NET

### Organizar usando directivas

Estas reglas de formato se refieren a la clasificación y visualización de directivas *`using`* y declaraciones *`Imports`*.

- *Ordenar System.* *`Using`* *directivas alfabéticamente* y colocarlas antes que otras directivas using.

  ```csharp
  //Right
  using System.Collections.Generic;
  using System.Threading.Tasks;
  using Octokit;
  ```

  ```csharp
  //Wrong
  using System.Collections.Generic;
  using Octokit;
  using System.Threading.Tasks;
  ```

- Do not place a blank line between using directive groups.

  ```csharp
  //Right
  using System.Collections.Generic;
  using System.Threading.Tasks;
  using Octokit;
  ```

  ```csharp
  //Wrong
  using System.Collections.Generic;
  using System.Threading.Tasks;

  using Octokit;
  ```

### Configuración de formato de C#

Las reglas de formato de esta sección se aplican solo al código C#.

#### Opciones de nueva línea

Estas reglas de formato se refieren al uso de nuevas líneas para formatear el código.

- Requiere que las llaves estén en una nueva línea para todas las expresiones (estilo "Allman").

  ```csharp
  //Right
  void MyMethod()
  {
      if (...)
      {
          ...
      }
  }
  ```

  ```csharp
  //Wrong
  void MyMethod() {
      if (...) {
          ...
      }
  }
  ```

- Coloque las declaraciones else en una nueva línea.

  ```csharp
  //Right
  if (...) 
  {
      ...
  }
  else 
  {
      ...
  }
  ```

  ```csharp
  //Wrong
  if (...) {
      ...
  } else {
      ...
  }
  ```

- Coloque declaraciones de captura en una nueva línea.

  ```csharp
  //Right
  try 
  {
      ...
  }
  catch (Exception e) 
  {
      ...
  }
  ```

  ```csharp
  //Wrong
  try {
      ...
  } catch (Exception e) {
      ...
  }
  ```

- Exigir que las declaraciones finalmente estén en una nueva línea después de la llave de cierre.

  ```csharp
  //Right
  try 
  {
      ...
  }
  catch (Exception e) 
  {
      ...
  }
  finally 
  {
      ...
  }
  ```

  ```csharp
  //Wrong
  try {
      ...
  } catch (Exception e) {
      ...
  } finally {
      ...
  }
  ```

- Requerir que los miembros de los inicializadores de objetos estén en líneas separadas

  ```csharp
  //Right
  var z = new B()
  {
      A = 3,
      B = 4
  }
  ```

  ```csharp
  //Wrong
  var z = new B()
  {
      A = 3, B = 4
  }
  ```

- Requerir que los miembros de tipos anónimos estén en líneas separadas

  ```csharp
  //Right
  var z = new
  {
      A = 3,
      B = 4
  }
  ```

  ```csharp
  //Wrong
  var z = new
  {
      A = 3, B = 4
  }
  ```

- Requerir que los elementos de las cláusulas de expresión de consulta estén en líneas separadas

  ```csharp
  //Right
  var q = from a in e
          from b in e
          select a * b;
  ```

  ```csharp
  //Wrong
  var q = from a in e from b in e
          select a * b;
  ```

#### Opciones de sangría

Estas reglas de formato se refieren al uso de sangría para formatear el código.

- Indent *`switch`* case contents

  ```csharp
  //Right
  switch(c) 
  {
      case Color.Red:
          Console.WriteLine("The color is red");
          break;
      case Color.Blue:
          Console.WriteLine("The color is blue");
          break;
      default:
          Console.WriteLine("The color is unknown.");
          break;
  }
  ```

  ```csharp
  //Wrong
  switch(c) {
      case Color.Red:
      Console.WriteLine("The color is red");
      break;
      case Color.Blue:
      Console.WriteLine("The color is blue");
      break;
      default:
      Console.WriteLine("The color is unknown.");
      break;
  }
  ```

- Indent *`switch`* labels

  ```csharp
  //Right
  switch(c) 
  {
      case Color.Red:
          Console.WriteLine("The color is red");
          break;
      case Color.Blue:
          Console.WriteLine("The color is blue");
          break;
      default:
          Console.WriteLine("The color is unknown.");
          break;
  }
  ```

  ```csharp
  //Wrong
  switch(c) {
  case Color.Red:
      Console.WriteLine("The color is red");
      break;
  case Color.Blue:
      Console.WriteLine("The color is blue");
      break;
  default:
      Console.WriteLine("The color is unknown.");
      break;
  }
  ```

- Las etiquetas se colocan en la misma sangría que el contexto actual

  ```csharp
  //Right
  class C
  {
      private string MyMethod(...)
      {          
          if (...) 
          {
              goto error;
          }
          error:
          throw new Exception(...);
      }
  }
  ```

  ```csharp
  //Wrong
  class C
  {
      private string MyMethod(...)
      {
          if (...) {
              goto error;
          }
  error:
          throw new Exception(...);
      }
  }
  ```

  ```csharp
  //Wrong
  class C
  {
      private string MyMethod(...)
      {
          if (...) {
              goto error;
          }
      error:
          throw new Exception(...);
      }
  }
  ```

#### Opciones de espaciado

Estas reglas de formato se refieren al uso de caracteres de espacio para formatear el código.

- Eliminar espacio entre el elenco y el valor

  ```csharp
  //Right
  int y = (int)x;
  ```

  ```csharp
  //Wrong
  int y = (int) x;
  ```

- Coloque un carácter de espacio después de una palabra clave en una declaración de flujo de control, como un bucle *`for`*

  ```csharp
  //Right
  for (int i;i<x;i++) { ... }
  ```

  ```csharp
  //Wrong
  for(int i;i<x;i++) { ... }
  ```

- Coloque un carácter de espacio antes de los dos puntos para las bases o interfaces en una declaración de tipo

  ```csharp
  //Right
  interface I
  {

  }

  class C : I
  {

  }
  ```

  ```csharp
  //Wrong
  interface I
  {

  }

  class C: I
  {

  }
  ```

- Coloque un carácter de espacio después de los dos puntos para bases o interfaces en una declaración de tipo

  ```csharp
  //Right
  interface I
  {

  }

  class C : I
  {

  }
  ```

  ```csharp
  //Wrong
  interface I
  {

  }

  class C :I
  {

  }
  ```

- Insertar espacio antes y después del operador binario

  ```csharp
  //Right
  return x * (x - y);
  ```

  ```csharp
  //Wrong
  return x*(x-y);
  ```

  ```csharp
  //Wrong
  return x  *  (x-y);
  ```

- Eliminar los espacios después del paréntesis de apertura y antes del paréntesis de cierre de una lista de parámetros de declaración de método
  
```csharp
  //Right
  void Bark(int x) { ... }
  ```

  ```csharp
  //Wrong
  void Bark( int x ) { ... }
  ```

- Quite el espacio entre paréntesis de la lista de parámetros vacía para una declaración de método

  ```csharp
  //Right
  void Goo()
  {
      Goo(1);
  }

  void Goo(int x)
  {
      Goo();
  }
  ```

  ```csharp
  //Wrong
  void Goo( )
  {
      Goo(1);
  }

  void Goo(int x)
  {
      Goo();
  }

  ```

- Elimine los espacios entre el nombre del método y el paréntesis de apertura en la declaración del método

  ```csharp
  //Right
  void M() { }
  ```

  ```csharp
  //Wrong
  void M () { }
  ```

- Eliminar los caracteres de espacio después del paréntesis de apertura y antes del paréntesis de cierre de una llamada a método

  ```csharp
  //Right
  MyMethod(argument);
  ```

  ```csharp
  //Wrong
  MyMethod( argument );
  ```

- Eliminar el espacio dentro de los paréntesis de la lista de argumentos vacía

  ```csharp
  //Right
  void Goo()
  {
      Goo(1);
  }

  void Goo(int x)
  {
      Goo();
  }
  ```

  ```csharp
  //Wrong
  void Goo()
  {
      Goo(1);
  }

  void Goo(int x)
  {
      Goo( );
  }
  ```

- Eliminar el espacio entre el nombre de la llamada al método y el paréntesis de apertura

  ```csharp
  //Right
  void Goo()
  {
      Goo(1);
  }

  void Goo(int x)
  {
      Goo();
  }
  ```

  ```csharp
  //Wrong
  void Goo()
  {
      Goo(1);
  }

  void Goo(int x)
  {
      Goo ();
  }
  ```

- Insertar espacio después de una coma

  ```csharp
  //Right
  int[] x = new int[] { 1, 2, 3, 4, 5 };
  ```

  ```csharp
  //Wrong
  int[] x = new int[] { 1,2,3,4,5 }
  ```

- Quitar espacio antes de una coma
  
```csharp
  //Right
  int[] x = new int[] { 1, 2, 3, 4, 5 };
  ```

  ```csharp
  //Wrong
  int[] x = new int[] { 1 , 2 , 3 , 4 , 5 };
  ```

- Inserte un espacio después de cada punto y coma en una instrucción for

  ```csharp
  //Right
  for (int i = 0; i < x.Length; i++)
  ```

  ```csharp
  //Wrong
  for (int i = 0;i < x.Length;i++)
  ```

- Quite el espacio antes de cada punto y coma en una instrucción for

  ```csharp
  //Right
  for (int i = 0; i < x.Length; i++)
  ```

  ```csharp
  //Wrong
  for (int i = 0 ; i < x.Length ; i++)
  ```

- Eliminar los caracteres de espacio extra en las declaraciones de declaración

  ```csharp
  //Right
  int x = 0;
  ```

  ```csharp
  //Wrong
  int    x    =    0   ;
  ```

- Quite el espacio antes de abrir los corchetes *`[`*

  ```csharp
  //Right
  int[] numbers = new int[] { 1, 2, 3, 4, 5 };
  ```

  ```csharp
  //Wrong
  int [] numbers = new int [] { 1, 2, 3, 4, 5 };
  ```

- Eliminar espacio entre corchetes vacíos*`[]`*

  ```csharp
  //Right
  int[] numbers = new int[] { 1, 2, 3, 4, 5 };
  ```

  ```csharp
  //Wrong
  int[ ] numbers = new int[ ] { 1, 2, 3, 4, 5 };
  ```

- Quite los caracteres de espacio en corchetes que no estén vacíos *`[0]`*

  ```csharp
  //Right
  int index = numbers[0];
  ```

  ```csharp
  //Wrong
  int index = numbers[ 0 ];
  ```

#### Opciones de envoltura

Estas reglas de formato se refieren al uso de líneas simples frente a líneas separadas para sentencias y bloques de código.

- Deje declaraciones y declaraciones de miembros en diferentes líneas

  ```csharp
  //Right
  int i = 0;
  string name = "John";
  ```

  ```csharp
  //Wrong
  int i = 0; string name = "John";
  ```

- Deje el bloque de código en una sola línea

  ```csharp
  //Right
  public int Foo { get; set; }
  ```

  ```csharp
  //Wrong
  public int MyProperty
  {
      get; set;
  }
  ```

## Convenciones de nombres

- Las constantes se nombran solo en mayúsculas con un delimitador *`_`*

  ```csharp
  //Right
  const int TEST_CONSTANT = 1;
  ```

  ```csharp
  //Wrong
  const int Test_Constant = 1;
  ```

- Los campos con acceso *`público`* se conocen como notación PascalCase

  ```csharp
  //Right
  public int TestField;
  ```

  ```csharp
  //Wrong
  public int testField;
  ```

- Los nombres de interfaz deben estar en notación PascalCase y tener el prefijo *`I`*

  ```csharp
  //Right
  public interface ITestInterface;
  ```

  ```csharp
  //Wrong
  public interface testInterface;
  ```

- Los nombres de clases, estructuras, métodos, enumeraciones, eventos, propiedades, espacios de nombres y delegados deben estar en notación PascalCase

  ```csharp
  //Right
  public class SomeClass;
  ```

  ```csharp
  //Wrong
  public class someClass;
  ```

- Asignado al parámetro de un tipo genérico un nombre descriptivo en la notación PascalCase, a menos que una letra y un nombre descriptivo no tengan valor práctico

  ```csharp
  //Right
  public interface ISessionChannel<TSession> { /*...*/ }
  public delegate TOutput Converter<TInput, TOutput>(TInput from);
  public class List<T> { /*...*/ }
  ```

- Utilice el nombre del parámetro type *`T`* para los tipos que contienen solo un parámetro de tipo de letra única

  ```csharp
  //Right
  public int IComparer<T>() { return 0; }
  public delegate bool Predicate<T>(T item);
  public struct Nullable<T> where T : struct { /*...*/ }
  ```

- Utilice el prefijo *`T`* para los nombres descriptivos de los parámetros de tipo

  ```csharp
  //Right
  public interface ISessionChannel<TSession>
  {
      TSession Session { get; }
  }
  ```

  Especifique las restricciones asociadas con el parámetro de tipo en su nombre. Por ejemplo, un parámetro de restricción *`ISession`* puede llamarse *`TSession`*.

- Private and protected class fields must begin with the prefix *`_`*

  ```csharp
  //Right
  private int _testField;
  protected int _testField;
  ```

  ```csharp
  //Wrong
  private int testField;
  protected int testField;
  ```

- Todos los demás elementos de código, como variables, parámetros de método y campos de clase (excepto los abiertos) se nombran en notación camelCase.

  ```csharp
  //Right
  var testVar = new Object();
  public void Foo(int firstParam, string secondParam)
  ```

  ```csharp
  //Wrong
  var TestVar = new Object();
  public void Foo(int FirstParam, string SecondParam)
  ```
