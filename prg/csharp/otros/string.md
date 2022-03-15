---
title: Programación Orientada a Objetos
layout: unit
---
# Clase String
Esta clase representa texto como una secuencia de caracteres.
## Propiedades
### Chars[]
```csharp 
public char this[int index] { get; }
```
Obtiene el _char_ situado en la posición _index_.
### Length
```csharp 
public int Length { get; }
```
Obtiene el número de caracteres de la cadena.
## Métodos
### CompareTo
```csharp 
public int CompareTo (string? strB);
```
Compara esta instancia con la cadena _strB_ e indica si la posición de esta instancia es anterior, posterior o igual que la posición de la cadena especificada.
Si el valor devuelto es:
-	Menor que cero: _strA_ precede a _strB_ en el criterio de ordenación.
-	Cero: _strA_ se produce en la misma posición que _strB_ en el criterio de ordenación.
-	Mayor que cero: _strA_ sigue a _strB_ en el criterio de ordenación.

El criterio de ordenación por defecto es el alfabético.

### Contains
```csharp 
public bool Contains (char value);
```
Devuelve un valor que indica si el carácter _value_ aparece dentro de la cadena.
```csharp 
public bool Contains (string value);
```
Devuelve un valor que indica si la subcadena _value_ aparece dentro de la cadena.
### EndsWith
```csharp 
public bool EndsWith (char value);
```
Determina si el final de esta instancia de cadena coincide con el carácter _value_.
```csharp 
public bool EndsWith (string value);
```
Determina si el final de esta instancia de cadena coincide con la cadena _value_.
### IndexOf
```csharp 
public int IndexOf (string value, int startIndex, int count);
```
Indica la posición de la primera aparición de la cadena _value_. La búsqueda comienza en la posición _startIndex_ y examina un número de posiciones _count_. Devuelve -1 si no hay ninguna aparición.
### Insert
```csharp 
public string Insert (int startIndex, string value);
```
Devuelve una nueva cadena en la que se inserta la cadena _value_ en la posición _startIndex_ de la instancia.
### LastIndexOf
```csharp 
public int LastIndexOf (string value, int startIndex, int count);
```
Indica la posición de la última aparición de la cadena _value_. La búsqueda se inicia en la posición _startIndex_ y continúa hacia atrás hacia el principio de la cadena durante un número especificado de posiciones de caracteres _count_.
### Remove
```csharp 
public string Remove (int startIndex, int count);
```
Devuelve una nueva cadena en la que se ha eliminado un número de caracteres _count_ a partir de la posición _startIndex_.
### Replace
```csharp 
public string Replace (string oldValue, string newValue);
```
Devuelve una nueva cadena en la que todas las apariciones de _oldValue_ se reemplazan por _newValue_.
### Split
```csharp 
public string[] Split (char separator);
```
Divide una cadena en subcadenas en función del separador indicado.
### StartsWith
```csharp 
public bool StartsWith (string value);
```
Determina si el principio de esta instancia de cadena coincide con la cadena especificada.
### Substring
```csharp 
public string Substring (int startIndex);
```
Devuelve una subcadena de la instancia. La subcadena empieza en la posición _startIndex_ y continúa hasta el final de la cadena.
```csharp 
public string Substring (int startIndex, int length);
```
Devuelve una subcadena de la instancia. La subcadena empieza en la posición _startIndex_ y tiene una longitud _length_.
### ToLower
```csharp 
public string ToLower ();
```
Devuelve una copia de esta cadena convertida en minúsculas.
### ToUpper
```csharp 
public string ToUpper ();
```
Devuelve una copia de esta cadena convertida en mayúsculas.
### ToCharArray
```csharp 
public char[] ToCharArray ();
```
Copia los caracteres del _string_ un _array_ de caracteres.
### Trim
```csharp 
public string Trim ();
```
Quita todos los caracteres de espacio en blanco del principio y el final de la cadena de texto.


## Métodos estáticos
### Compare
```csharp 
public static int Compare (string? strA, string? strB);
```
Compara dos objetos String especificados y devuelve un entero que indica su posición relativa en el criterio de ordenación.
-	Menor que cero: strA precede a strB en el criterio de ordenación.
-	Cero: strA se produce en la misma posición que strB en el criterio de ordenación.
-	Mayor que cero: strA sigue a strB en el criterio de ordenación.

### IsNullOrEmpty
```csharp 
public static bool IsNullOrEmpty (string? value);
```
Indica si el valor de la cadena es _null_ o una cadena vacía ("").

## Bibliografía

https://docs.microsoft.com/es-es/dotnet/api/system.string?view=net-5.0