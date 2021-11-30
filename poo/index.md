---
title: Programación Orientada a Objetos
layout: unit
---
# Programación Orientada a Objetos

La programación orientada a objetos, en adelante POO, es un paradigma de programación que se basa en el concepto de objeto. Un programa en ejecución consta de una serie de objetos relacionados que pueden comunicarse entre sí.

La POO tiene por objeto organizar el código de forma similar a cómo el ser humano organiza y clasifica la realidad que le rodea.

Decimos que los gatos tienen bigotes, patas, pelo de un determinado color, que maullan y ronronean. Así pues, los gatos tienen una serie de características y comportamientos en común.

Los empleados de una empresa tienen nombre, salario y la posibilidad de promocionar o pedirse vacaciones. Vemos que los empleados de una empresa también tienen una serie de características y comportamientos en común.

La POO se basa en organizar el código en clases en las que se definen las características y comportamientos que tienen en común los objetos de dicha clase.

## Clases
Las clases son una especie de plantillas que nos permiten definir cuáles son las características y comportamientos de los objetos creados a partir de ella.

La sintaxis de una clase es la siguiente:

    class NombreClase{
        // definición de la clase
    }

Donde _NombreClase_ es el nombre de la clase.

> Los nombres de las clases siempre empiezan en mayúscula.

Dentro de la clase definiremos sus características mediante el uso de campos o atributos. Los comportamientos se definen mediante el uso de métodos.

Para continuar con la explicación pondremos un ejemplo que desarrollaremos a lo largo de la unidad. Imaginemos que vamos a desarrollar un programa para gestionar cuentas bancarias y que las características y comportamientos que queremos representar son los siguientes:

- Características: número de cuenta, titular y saldo.
- Comportamientos: realizar ingreso, realizar reintegro y cambiar titular, obtener información.

Por supuesto, se nos podrían ocurrir mil características y comportamientos diferentes de una cuenta, cuáles vamos a considerar dependerá del problema que queramos resolver.

## Campos o atributos
Mediante los campos o atributos representaremos las características de una clase. Las sintaxis general es la siguiente:

    class NombreClase{
        tipo atributo1;
        tipo atributo2;
        ...
    }

Donde _tipo_ es el tipo del atributo y _atributo1_ su identificador. Como podemos ver, no dejan de ser declaraciones de variables.

Podemos inicializar los atributos con un valor por defecto de la siguiente forma:

    class NombreClase{
        tipo atributo1 = valor;
        ...
    }

Los atributos son variables que están declaradas dentro de la clase, pero fuera de los métodos. Siempre las declararemos al inicio de la clase.

    class Cuenta{
        string numeroCuenta;
        string titular;
        float saldo;
    }

### Ámbito de los atributos.
Como ocurre con el resto de variables, el ámbito de los atributos viene determinado por el bloque de llaves {} que lo contiene, por tanto los atributos pueden ser accedidos desde cualquier método de la clase.

## Métodos

Los comportamientos de una clase se definen mediante el uso de métodos, que no son más que funciones que se implementan dentro de una clase.

> Al conjunto de atributos y métodos de una clase se le llama miembros de la clase.

### Ocultación de atributos

## Objetos
### Creación de una instancia
## Constructores
### Constructor genérico this
## Modificadores de acceso y visibilidad
## Atributos y métodos estáticos
