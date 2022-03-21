---
title: Herencia, clases abstractas e interfaces
layout: unit
---
# Herencia, clases abstractas e interfaces

# Introducción

La herencia es una característica de la programación orientada a objetos que permite que diferentes miembros (campos, propiedades o métodos) de una clase se transmitan a otra, permitiéndonos reutilizar el código.

La clase de la que se hereda se denomina clase padre, superclase o clase base, y la clase que hereda es conocida como clase hija, subclase o clase derivada.

La subclase dispone de los miembros heredados de la superclase y generalmente se amplía añadiendo sus propios miembros.

# Conceptos básicos
En C# una clase hereda de otra de la siguiente forma:

```csharp
public class Empleado{
    // definición de la clase Empleado
}

public class Comercial : Empleado{
    // definición de la clase Comercial
}
```
En este caso la clase _Comercial_ hereda de _Empleado_. Siempre hay que recordar que la herencia es una relación de tipo _es un_. Comercial puede heredar de empleado porque un comercial _es un_ empleado sin embargo un empleado _no es_ un comercial.

En lenguajes como C++ es posible heredar de múltiples clases, sin embargo en Java y C# esto no es posible. Esto no impide que podamos generar una jerarquía de clases: La clase _LibroElectronico_ y _LibroDigital_ heredan de _Libro_ que a su vez hereda de _Artículo_.

## Modificadores de accesibilidad _protected_

Una clase hereda todos los miembros de la clase padre, aunque aquellos que sean _private_ no serán accesibles desde la subclase.

Con la herencia aparece un nuevo tipo de modificador de accesibilidad que podemos aplicar a los miembros de una clase: _protected_.

El uso de _protected_ permite que un miembro sea visible desde la propia clase y sus subclases pero no desde clases que no sean subclases.

```csharp
public class C {
	private int a;
	int b;
	protected int c;
	public int d;
}
```
Dado el ejemplo anterior:

- _a_ y _b_ son accesibles únicamente desde la propia clase. En el caso de _b_ hay que recordar que el modificador de accesibilidad por defecto es _private_.
- _c_ es accesible desde la clase _C_ y sus subclases.
- _d_ es accesible desde cualquier clase.

## Constructor base
Si heredamos de una clase que no tiene constructores definidos (en realidad por defecto siempre tendrá el constructor vacío) en la clase derivada no será obligatorio definir un constructor ni llamar al constructor padre.

En el siguiente ejemplo, puesto que la clase _Empleado_ no tiene constructor, no estamos obligados a definir un constructor en la clase _Comercial_.

```csharp
    class Empleado
    {
        public string Nombre { get; set; }
        public float SalarioBrutoMensual { get; set; }
        public float Irpf { get; set; }
    }

    class Comercial : Empleado
    {
        public float TotalVentas { get; set; }
        public float PorcentajeComision { get; set; }
       
    }
```
En el momento que la clase padre tiene algún constructor estaremos obligados a definir un constructor en la clase derivada. Este constructor deberá llamar a uno de los constructores de su clase padre mediante la palabra reservada _base_ como se muestra a continuación:
```csharp
class Empleado
{
    public string Nombre { get; set; }
    public float SalarioBrutoMensual { get; set; }
    public float Irpf { get; set; }

    public Empleado (string nombre, float salarioBrutoMensual)
    {
        Nombre = nombre;
        SalarioBrutoMensual = salarioBrutoMensual;
    }
}

class Comercial : Empleado
{
    public float TotalVentas { get; set; }
    public float PorcentajeComision { get; set; }

    public Comercial(string nombre, float salarioBrutoMensual, float totalVentas): base(nombre, salarioBrutoMensual)
    {
        TotalVentas = totalVentas;
        PorcentajeComision = 0.05f;
    }   
}
```
# Polimorfismo
Es la capacidad de una entidad de tomar diferentes formas en distintos instantes de tiempo. Nos permite programar de manera general en lugar de programar de manera específica.

## Polimorfismo ad-hoc o polimorfismo de sobrecarga
Consiste en que dos o más métodos compartan el mismo identificador pero teniendo una lista de parámetros diferentes (ya sea por número de parámetros o su tipo).

Este tipo de polimorfismo se utiliza mucho, por ejemplo, en los constructores.

```csharp
class Empleado
{
    public string Nombre { get; set; }
    public float SalarioBrutoMensual { get; set; }
    public float Irpf { get; set; }
    public Empleado (string nombre, float salarioBrutoMensual)
    {
        Nombre = nombre;
        SalarioBrutoMensual = salarioBrutoMensual;
    }
    public Empleado(string nombre, float salarioBrutoMensual, float irpf)
    {
        Nombre = nombre;
        SalarioBrutoMensual = salarioBrutoMensual;
        Irpf = irpf;
    }
}
```
Pero se puede aplicar a cualquier método. Por ejemplo, el método _WriteLine_ de la clase _Console_ tiene 19 sobrecargas para poder mostrar por pantalla variables de diferentes tipos.

## Polimorfismo de inclusión, _overriding_ o sobreescritura

En ocasiones puede interesar modificar el comportamiento de la clase padre. Para ello definimos un método en la clase hija con el mismo identificador y parámetros que el método de la clase padre que queremos modificar. Este mecanismo se conoce como sobreescritura u _overriding_.

Imaginemos que nuestra clase _Empleado_ tiene un método para calcular el salario neto mensual:

```csharp
    class Empleado
    {
        ...
        
        public float CalcularSalarioNeto()
        {
            return SalarioBrutoMensual - (SalarioBrutoMensual * Irpf);
        }
        ...
    }
```

Sin embargo nos dicen que el cálculo del salario de un comercial es diferente ya que para su cálculo también se tiene en cuenta la comisión de las ventas que haga. Es decir, necesitamos que la clase _Comercial_ también tenga un método _CalcularSalarioNeto_ cuyo cuerpo será diferente al del método padre.

Para poder sorbeescribir el método en primer lugar tendremos que cambiar la definición del método _CalcularSalarioNeto_ en la clase _Empleado_ para añadirle el modificador _virtual_ del siguiente modo:

```csharp
    class Empleado
    {
        ...
        
        public virtual float CalcularSalarioNeto()
        {
            return SalarioBrutoMensual - (SalarioBrutoMensual * Irpf);
        }
        ...
    }
```
En la clase derivada podremos sobreescribir el método haciendo uso de la palabra reservada _override_:

```csharp
class Comercial : Empleado
{
    ...
    public override double CalcularSalarioNeto()
    {
        return (SalarioBrutoMensual - (SalarioBrutoMensual * Irpf)) + (TotalVentas * PorcentajeComision);
    }
    ...
}
```

Si nos fijamos en el código del método _CalcularSalarioNeto()_ de la clase _Comercial_ parte del cálculo del salario es igual al cálculo del salario de un _Empleado_. Con la palabra reservada _base_ podemos acceder a los miembros de la clase padre, por lo que podríamos llamar a cualquiera de sus métodos incluso estando sobreescritos.


```csharp
class Comercial : Empleado
{
    ...
    public override double CalcularSalarioNeto()
    {
        return base.CalcularSalarioNeto() + (TotalVentas * PorcentajeComision);
    }
    ...
}
```

##  Polimorfismo de asignación
Una misma variable puede hacer referencia a más de un tipo de clase, a este tipo de variables las llamaremos **polimórficas**. El conjunto de clases que pueden ser referenciadas está restringido por la herencia. Una variable de tipo A, puede referenciar a un objeto de tipo A y a un objeto de tipo B cuando haya una relación de herencia entre A y B.

```csharp
Empleado e1 = new Comercial("Juan", 1000, 100);
Comercial c = new Comercial("Julia", 2000, 200);
Empleado e2 = new Empleado("Andrés", 1500);
Comercial c2 = new Empleado("Isabel", 1500); // Error, asignación no permitida
```
El polimorfismo de asignación permite que podamos crear métodos como  _IncrementarSueldo_ que pueden ser utilizados con cualquier tipo de empleado, pudiendo así reutilizar su código.

```csharp
private static float bonusProductividad = 100.0f;
static void Main(string[] args)
{
    Comercial c = new Comercial("Juan", 1000, 100);
    IncrementarSueldo(c, 500);
    Console.ReadKey();
}

static void IncrementarSueldo (Empleado e, float productividad)
{
    float incremento = productividad * bonusProductividad;
    e.SalarioBrutoMensual += incremento;
}
```
En el ejemplo anterior al método _IncrementarSueldo_ podemos pasarle como parámetro cualquier empleado incluídos los comerciales.

Este tipo de polimorfismo también nos permite almacenar diferentes tipos de empleados en una única lista, independientemente de que sean comerciales, técnicos o administrativos. De esta forma evitamos tener una lista por cada tipo de empleado.

## Conversión o _cast_ de tipos
Debido al polimorfismo de asignación hemos visto que podemos realizar la siguiente asignación:

```csharp
Empleado e1 = new Comercial("Juan", 1000, 100);
```

A este tipo de conversión se le llama “conversión hacia arriba” y en él se gana generalidad pero perdemos el acceso a los miembros concretos de la subclase. Por ejemplo, a partir de la variable _e1_ no podemos acceder a las propiedades _TotalVentas_ o _PorcentajeComision_. Tampoco podremos acceder a los métodos del comercial a no ser que éstos sobreescriban algún método de la clase padre. Esto lo veremos más adelante en el apartado "Selección dinámica de métodos". 

Si se quiere recuperar el acceso a los miembros de la subclase será necesario realizar una “conversión hacia abajo” mediante un cambio de tipo. Dicha conversión se lleva a cabo mediante una operación de _casting_.

```csharp
Empleado e1 = new Comercial("Juan", 1000, 100);
Comercial c1 = (Comercial) e1;
```
La operación de conversión producirá una excepción _InvalidCastException_ si intentamos realizar una conversión que no es válida.

En C# también disponemos del operador _as_  para realizar esta conversión. La diferencia con la operación de _cast_ es que _as_ devuelve _null_ en vez de producir una excepción en caso de que no pueda realizar la conversión.
```csharp
Comercial c1 = e1 as Comercial;
```
## Selección dinámica de métodos

Dado el siguiente fragmento de código, a la hora de ejecutar el método _CalcularSalarioNeto_ el entorno de ejecución comprobará que dicho método existe en la clase _Empleado_ y que está sobreescrito en la clase _Comercial_. En este caso el método que se ejecutará será el de la clase _Comercial_ y no el de _Empleado_. Este mecanismo recibe el nombre de selección dinámica de métodos.
```csharp
static void Main(string[] args)
{
    Empleado e = new Comercial("Juan", 1000, 100);
    e.Irpf = 0.1f;
    Console.WriteLine(e.CalcularSalarioNeto());
    Console.ReadKey();
}
```
# La clase Object
En C# absolutamente todas las clases descienden de la clase _Object_. Incluso cualquier clase que implementemos nosotros. Esta herencia se realiza por defecto sin necesidad de especificar nada.

Con ello se consigue:
- Que todas las clases implementen un conjunto de métodos que son de uso universal en C#. Estos métodos están destinados a realizar comparaciones entre objetos, comprobar si son iguales o representar un objeto como una cadena de caracteres.
- Poder referenciar cualquier objeto, de cualquier tipo, mediante una variable de tipo _Object_.

Por ese motivo podemos hacer la siguiente asignación.

```csharp
Object o = new Comercial("Juan", 1000, 100);
```
_Comercial_ hereda de _Empleado_ y _Empleado_ hereda de _Object_.

## Método ToString
La clase _Object_ implementa el método virtual _ToString_. La implementación por defecto devuelve el nombre completo de la clase. Por eso, si ejecutamos lo siguiente:

```csharp
static void Main(string[] args)
{
    Empleado e = new Empleado("Juan", 1000, 10);
    Console.WriteLine(e);
    Console.ReadKey();
}
```
Se muestra por pantalla:
```csharp
U8.Empleado
```
Si nos fijamos en la sobrecarga del método _WriteLine_ que se está utilizando (pasando el cursor por encima), veremos que se está llamando la sobrecarga del método que recibe por parámetro un objeto de tipo _Object_. Internamente lo que hace el método _WriteLine_ es llamar al método _ToString_ del objeto que recibe por parámetro y la cadena que devuelve dicho método es lo que muestra por pantalla.

Si queremos cambiar este comportamiento podemos sobreescribir en la clase _Empleado_ el método _ToString_.

```csharp
public override string ToString()
{
    return "Nombre: " + Nombre + " Bruto: " + SalarioBrutoMensual + " Neto: " + CalcularSalarioNeto();
}
```
Si ejecutamos de nuevo el código anterior ahora se mostrará por pantalla:
```csharp
Nombre: Juan Bruto: 1000 Neto: 900
```
<!--
## Método Equals
Imaginemos que tenemos una clase _Punto_ con dos propiedades _X_ y _Y_ y creamos dos instancias del siguiente modo:
```csharp
Punto p1 = new Punto();
p1.X = 10; p1.Y = 20;
Punto p2 = new Punto();
p2.X = 10; p2.Y = 20;
```
Si comparamos las instancias con el operador == obtendremos que son diferentes ya que sus referencias son distintas.
```csharp
Console.WriteLine(p1==p2); // Muestra falso
```
Puede interesarnos crear un método para comparar dos objetos más allá de comprobar si el objeto referenciado es el mismo. Para ello podemos sobreescribir el método _Equals_ de la clase _Object_.

```csharp
public virtual bool Equals (object? obj);
```
https://stackoverflow.com/questions/371328/why-is-it-important-to-override-gethashcode-when-equals-method-is-overridden
-->

## Método _GetType_, operador _typeof_ e _is_
El método _GetType_ permite obtener el tipo de una instancia en tiempo de ejecución.
```csharp
static void Main(string[] args)
{
    Empleado e = new Empleado("Juan", 1000, 0.1f);
    Console.WriteLine(e.GetType()); // Muestra U8.Empleado
    Console.ReadKey();
}
```
Mediante el operador _typeof_ obtenemos el tipo de una clase. 
```csharp
static void Main(string[] args)
{
    Type t = typeof(Empleado);
    Console.WriteLine(t); // Muestra U8.Empleado
    Console.ReadKey();
}
```
Podemos utilizar el _GetType_ y _typeof_ para saber si una instancia es de un determinado tipo o no.

```csharp
static void Main(string[] args)
{
    // Caso A
    Empleado e1 = new Empleado("Juan", 1000, 0.1f);
    Console.WriteLine(e1.GetType() == typeof(Empleado)); // Muestra true
    // Caso B
    Comercial c1 = new Comercial("Sonia", 1200, 500);
    Console.WriteLine(c1.GetType() == typeof(Empleado)); // Muestra false
    // Caso C
    Empleado e2 = new Comercial("Rubén", 1100, 300);
    Console.WriteLine(e2.GetType() == typeof(Empleado)); // Muestra false
    Console.ReadKey();
}
```
- Caso A: Puesto que _e1_ es una variable de tipo _Empleado_ la comparación da como resultado _true_.
- Caso B: _c1.GetType()_ devuelve _U8.Comercial_, mientras que typeof(Empleado) devuelve _U8.Empleado_. La comparación da como resultado _false_ aunque exista una relación herencia entre las clases.
- Caso C: Este es un caso especial ya que _e2.GetType()_ devuelve _U8.Comercial_ aunque se haya declarado como una variable de tipo _Empleado_. Por otra parte _typeof(Empleado)_ devuelve _U8.Empleado_ por lo que la comparación da como resultado _false_.

Para saber si una instancia es de una determinada clase pertenece a una jerarquía de herencias podemos utilizar el operador _is_.

```csharp
static void Main(string[] args)
{
    // Caso A
    Empleado e1 = new Empleado("Juan", 1000, 0.1f);
    Console.WriteLine(e1 is Empleado); // Muestra true
    // Caso B
    Comercial c1 = new Comercial("Sonia", 1200, 500);
    Console.WriteLine(c1 is Empleado); // Muestra true
    // Caso C
    Empleado e2 = new Comercial("Rubén", 1100, 300);
    Console.WriteLine(e2 is Empleado); // Muestra true
    Console.ReadKey();
}
```

# Clases abstractas

Cuando creamos una herencia podemos encontrarnos con uno o varios métodos que sabemos que deben tener todas las subclases pero que no sabemos o podemos implementar en la superclase. En ese caso podemos definir el método en la superclase pero delegar su implementación a las subclases. Se dirá que el método es abstracto. El resto de métodos (no abstractos) y propiedades de la clase se heredarán normalmente.

Para declarar un método abstracto se antepone el modificador _abstract_ y se sustituyen las llaves {} por un punto y coma. Las clases que tengan un método abstracto tendrán que declararse a su vez abstractas y no serán instanciables.

```csharp
abstract class Animal
{
    public int Edad { get; set; }
    public string Nombre { get; set; }
    public abstract void Sonido();
}
```
Las subclases se encargarán de implementar los métodos abstractos. Para ello se utilizará la palabra clave _override_ como se muestra a continuación. 

```csharp
    class Perro : Animal
    {
        public override void Sonido()
        {
            Console.WriteLine("WOW!");
        }
    }
```

Si una clase hereda de una clase abstracta y deja alguno de sus métodos abstractos sin implementar entonces también será abstracta.
