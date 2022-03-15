---
title: Herencia, clases abstractas e interfaces
layout: unit
---
# Herencia, clases abstractas e interfaces

## Introducción

La herencia es una característica de la programación orientada a objetos que permite que diferentes miembros (campos, propiedades o métodos) de una clase se transmitan a otra, permitiéndonos reutilizar el código.

La clase de la que se hereda se denomina clase padre, superclase o clase base, y la clase que hereda es conocida como clase hija, subclase o clase derivada.

La subclase dispone de los miembros heredados de la superclase y, generalmente, se amplía añadiendo sus propios miembros.

Podemos indicar que una clase hereda de otra de la siguiente forma:

```csharp
public class Empleado{
    // definición de la clase Empleado
}

public class Comercial : Empleado{
    // definición de la clase Comercial
}
```
En este caso la clase _Comercial_ hereda de _Empleado_. Siempre hay que recordar que la herencia es una relación de tipo _es un_. Comercial puede heredar de empleado porque un comercial _es un_ empleado.

En lenguajes como C++ es posible heredar de múltiples clases, sin embargo en Java y C# esto no es posible. Esto no impide que podamos generar una jerarquía de clases: La clase _LibroElectronico_ y _LibroDigital_ heredan de _Libro_ que a su vez hereda de _Artículo_.

# Modificadores de accesibilidad _protected_

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

- _a_ y _b_ son accesibles únicamente desde la propia clase.
- _c_ es accesible desde la clase _C_ y sus subclases.
- _d_ es visible desde cualquier clase.

# Constructor base
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

    public float CalcularSalarioNeto()
    {
        return SalarioBrutoMensual - (SalarioBrutoMensual * Irpf);
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

Sin embargo nos dicen que el cálculo del salario de un comercial es diferente, ya que se tiene en cuenta la comisión de las ventas que haga. Es decir, necesitamos que la clase _Comercial_ también tenga un método _CalcularSalarioNeto_ cuyo cuerpo será diferente al del método padre.

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

También nos permite poder almacenar diferentes tipos de empleados en una única lista, independientemente de que sean comerciales, técnicos o administrativos.

### Conversión o _cast_ de tipos
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

## Selección dinámica de métodos

Dado el siguiente fragmento de código, a la hora de ejecutar el método _CalcularSalarioNeto_ el entorno de ejecución comprobará que dicho método existe en la clase _Empleado_ pero que está redefinido el de la clase _Comercial_, puesto que la referencia almacenada en la variable _e_ realmente es de tipo _Comercial_ el método que se ejecutará será el de la clase _Comercial_. Este mecanismo recibe el nombre de selección dinámica de métodos.
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
- Que todas las clases implementen un conjunto de métodos que son de uso universal en C#, destinados a realizar comparaciones entre objetos, comprobar si son iguales o representar un objeto como una cadena de caracteres.
- Poder referenciar cualquier objeto, de cualquier tipo, mediante una clase de tipo _Object_.

Por ese motivo podemos hacer la siguiente asignación.

```csharp
Object o = new Comercial("Juan", 1000, 100);
```

## Método ToString
La clase _Object_ implementa el método _ToString_. La implementación por defecto devuelve el nombre completo de la clase. Por eso, si ejecutamos lo siguiente:

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
Si nos fijamos en la sobrecarga del método _WriteLine_ que se está utilizando (pasando el cursor por encima), veremos que se está llamando al método que recibe por parámetro un objeto de tipo _Object_. Internamente lo que hace el método _WriteLine_ es llamar al método _ToString_ del objeto que recibe por parámetro, la cadena que devuelve el método es lo que muestra por pantalla.

Si queremos cambiar este comportamiento podemos sobreescribir en la clase _Empleado_ el método _ToString_.

```csharp
public override string ToString()
{
    return "Nombre: " + Nombre + " Bruto: " + SalarioBrutoMensual + " Neto: " + CalcularSalarioNeto();
}
```
Si ejecutamos de nuevo el código anterior ahora se mostrará por pantalla:
Se muestra por pantalla:
```csharp
Nombre: Juan Bruto: 1000 Neto: 900
```

