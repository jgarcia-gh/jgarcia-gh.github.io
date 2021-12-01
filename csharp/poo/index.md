---
title: Programación Orientada a Objetos
layout: unit
---
# Programación Orientada a Objetos

La programación orientada a objetos, en adelante POO, es un paradigma de programación que tiene por objeto estructurar el código de forma similar a cómo el ser humano organiza y clasifica la realidad que le rodea. De esta forma se busca que el código sea más fácil de organizar, comprender y por tanto mantener.

La POO se basa en organizar el código en módulos denominados clases en las que se definen las características y comportamientos que tienen en común sus instancias o ejemplares.

Como su nombre indica, la POO gira entorno al concepto de objeto. Así pues, un programa en ejecución consta de una serie de objetos relacionados que se comunican entre sí.

## Clases
Las clases son una especie de plantillas que nos permiten definir cuáles son las características y comportamientos de los objetos creados a partir de ella. Podemos ver las clases como los moldes que nos permiten crear los objetos.

La sintaxis de una clase es la siguiente:
```csharp
class NombreClase{
    // definición de la clase
}
```
Donde _NombreClase_ es el nombre de la clase.

> Los nombres de las clases siempre empiezan en mayúscula.

Dentro de la clase definiremos sus características mediante el uso de **campos o atributos** y sus comportamientos mediante el uso de **métodos**.

Para continuar con la explicación pondremos un ejemplo que desarrollaremos a lo largo de la unidad. Imaginemos que vamos a desarrollar un programa para gestionar cuentas bancarias. Podríamos definir las siguientes características y comportamientos:

- Características: número de cuenta, titular y saldo.
- Comportamientos: realizar ingreso, realizar reintegro y cambiar titular, obtener información.

Por supuesto, se nos podrían ocurrir mil características y comportamientos mas, cuáles vamos a considerar dependerá del problema que queramos resolver.

## Campos o atributos
Mediante los campos o atributos representaremos las características de una clase. Las sintaxis general es la siguiente:
```csharp
    class NombreClase{
        tipo atributo1;
        tipo atributo2;
        ...
    }
```
Donde _tipo_ es el tipo del atributo y _atributo1_ su identificador. Como podemos ver, no dejan de ser declaraciones de variables.

Podemos inicializar los atributos con un valor por defecto de la siguiente forma:
```csharp
    class NombreClase{
        tipo atributo1 = valor;
        ...
    }
```
Los atributos son variables que están declaradas dentro de la clase, pero fuera de los métodos. Siempre las declararemos al inicio de la clase, antes de los métodos.

A continuación, se muestra la clase Cuenta con sus atributos:

```csharp
class Cuenta{
    string numeroCuenta;
    string titular;
    float saldo;
}
```

### Ámbito de los atributos.
Como ocurre con el resto de variables, el ámbito de los atributos viene determinado por el bloque de llaves {} que lo contiene, por tanto los atributos pueden ser accedidos desde cualquier método de la clase.

## Métodos

Los comportamientos de una clase se definen mediante el uso de métodos, que no son más que funciones que se implementan dentro de una clase.

A continuación, se muestra la clase Cuenta incluyendo sus métodos:

realizar ingreso, realizar reintegro y cambiar titular, obtener información.

```csharp
class Cuenta
{
    string numeroCuenta;
    string titular;
    float saldo;

    public void Ingresar(float cantidad)
    {
        saldo = saldo + cantidad;
    }

    public void Reintegrar(float cantidad)
    {
        saldo = saldo - cantidad;
    }

    public void CambiarTitular (string nuevoTitular)
    {
        titular = nuevoTitular;
    }

    public string ObtenerInformacion()
    {
       return numeroCuenta + " " + titular + " " + saldo + "€";
    }
}
```
Como se puede ver en el ejemplo anterior, los atributos son variables accesibles desde cualquier método.

> Al conjunto de atributos y métodos de una clase se le llama **miembros** de la clase.

> Las variables declaradas dentro de un método reciben el nombre de **variables locales**.

### Ocultación de atributos

Como hemos visto hasta ahora, no podemos declarar dos variables con el mismo identificador si se encuentran en el mismo ámbito o en ámbitos anidados.

```csharp
int n = int.Parse(Console.ReadLine());
if(n > 10)
{
    int n = 10; // Error: la variable n ya se ha declarado
}
```
```csharp
public void GenerarNumero(int n)
{
    int n = int.Parse(Console.ReadLine()); // Error: la variable n ya se ha declarado
}
```

Sin embargo existe una excepción: dentro de un método podemos declarar una variable con el mismo identificador que un atributo de la clase.

```csharp
class Articulo
{
    string nombre = "Pepito";

    public void MostrarNombre(string nombre) // No se produce un error
    {
        nombre = "Juanito";
        Console.WriteLine(nombre);
    }
}
```
En el ejemplo anterior, dentro del método _MostrarNombre_ ¿A qué variable se hace referencia cuando se utiliza la variable _nombre_?¿A la variable local, esto es, el parámetro del método o al atributo de la clase?.

Ante esta situación las variables locales tienen prioridad sobre el atributo. Se dice que la variable local **oculta al atributo**.

Por tanto, si llamamos al método _MostrarNombre_ se mostrará por pantalla _"Juanito"_ y el atributo _nombre_ seguirá valiendo _"Pepito"_.

Ante esta situación, ¿Cómo podemos hacer referencia al atributo en vez de la variable local? Para ello disponemos de la palabra reservada _this_ que permite hacer referencia un atributo de la clase incluso cuando ha sido ocultado por una variable local.

A continuación, se muestra un ejemplo de uso de la palabra reservada _this_.

```csharp
class Cuenta
{
    string numeroCuenta;
    string titular;
    float saldo;

    ...

    public void CambiarTitular (string titular)
    {
        this.titular = titular;
    }

    ...    

}
```
El ejemplo anterior _this.titular_ hace referencia al atributo _titular_, mientras que _titular_ hace referencia al parámetro del método. De esta forma es posible diferenciar a qué variable estamos haciendo referencia.

## Objetos

Hasta ahora hemos visto cómo crear las "plantillas" o "moldes" que nos van a permitir crear objetos. Hemos definido qué tiene una cuenta bancaria, pero aún no hemos creado ninguna.

### Creación de una instancia

Los elementos creados a partir de una clase se llaman **instancias** u **objetos**. Todos los objetos creados a partir de una clase tienen los mismos atributos y métodos, pero los atributos de cada objeto tiene sus propios valores.

Para crear una instancia de una clase en primer lugar es necesario declarar una variable. En el tipo de la variable escribiremos el nombre de la clase.

```csharp
NombreClase nombreVariable;
```
La variable _nombreVariable_ está declarada, pero no inicializada. Para poder utilizar la variable es imprescindible inicializarla. Para ello utilizaremos el operador _new_.

```csharp
nombreVariable = new NombreClase();
```
Por supuesto, podríamos haber declarado e inicializado la variable en una única línea:

```csharp
NombreClase nombreVariable = new NombreClase();
```
A partir de ahora, podemos acceder a los atributos y métodos de la instancia mediante el uso de un punto tras el nombre de la variable.

```csharp
NombreClase nombreVariable = new NombreClase();
nombreVariable.atributo1 = nuevoValor; // Asignamos un nuevo valor al atributo atributo1
Console.WriteLine(nombreVariable.atributo1); // Mostramos el valor del atributo atirbuto1
nombreVariable.metodo1(); // Llamamos al método metodo1 de la variable nombreVariable
```
Siguiendo con el ejemplo de las cuentas bancarias vamos a crear varias instancias de la clase _Cuenta_ en el método _Main_:

```csharp
static void Main(string[] args)
{
    Cuenta c1 = new Cuenta();
    Cuenta c2 = new Cuenta();

    c1.CambiarTitular("Andresito");
    c1.Ingresar(100);

    c2.CambiarTitular("Laurita");
    c2.Ingresar(200);

    Console.WriteLine(c2.ObtenerInformacion());
}
```
En el código anterior se crean dos instancias de la clase _Cuenta_. El titular de la primera cuenta pasa a ser Andresito quien ingresa 100€. La segunda cuenta pasa a ser de Laurita, quien hace un ingreso de 200€. Finalmente se muestra la información de la segunda cuenta por pantalla.

Si intentamos acceder a los atributos del mismo modo que lo hemos hecho con los métodos, veremos que se produce un error que nos indica que el atributo _saldo_ es inaccesible.

```csharp
Console.WriteLine(c1.saldo); // Error ya que no se puede acceder al atributo debido a su nivel de accesibilidad
```

## Modificadores de acceso
## Trabajando con referencias
## Constructores
### Constructor genérico this
## Atributos y métodos estáticos


Uso de clases en atributos, paso de parámetros, arrays, etc.
