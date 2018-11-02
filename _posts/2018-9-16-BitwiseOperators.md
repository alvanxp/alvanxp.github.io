---
tags:
  - c#
  - bitwise operators
layout: post
title: 'Bitwise Operations - Parte I'
category: c#
comments: true
---

Entender la manipulación de bits es util en escenario donde tenemos que usar menos cantidad de memoria para guardar datos o estados

# Attributo Flags

El Attributo Flags permite poder usar más de una option del enumerado y almacearlo en una variable, Por ejemplo el siguiente enum:

```csharp
[Flags]
public enum BookingOptions
{
  None = 0,
  EnSuite = 1,
  SeaView = 2,
  StairFreeAccess = 4,
  Breakfast = 8
}

```

Dados los valores del enum, podemos elegir uno o varios valores del enum, por ejemplo:

```csharp
BookingOptions bookingOptionsSelected = BookingOptions.SeaView | BookingOptions.Breakfast;

Console.WriteLine(bookingOptionsSelected);
//Output: SeaView, Breakfast
```

## Detras de escena

El atributo Flags permite aplicar el operador de bits Or entre los atributos, dado que cada item del enumerado tiene un valor binario:

|            | Breakfast&nbsp;&nbsp; | StairFreeAccess&nbsp;&nbsp; | SeaView&nbsp;&nbsp; | EnSuite&nbsp;&nbsp; |
|------------|-----------|-----------------|---------|---------|
| **Enum Value**&nbsp;&nbsp; | 8         | 4               | 2       | 1       |
| **Breakfast**&nbsp;&nbsp;  | 1         | 0               | 0       | 0       |
| **EnSuite**&nbsp;&nbsp;    | 0         | 0               | 1       | 0       |

se eligieron dos valores Breakfast con valor 8 y en binario 1000 y EnSuite con valor 2 y en binario 0010, entonces necesitamos combinar los valores en un solo byte

| &nbsp;       | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
|-----------------|---|---|---|---|
| **Breakfast**&nbsp;&nbsp;       | 1 | 0 | 0 | 0 |
| **EnSuite**&nbsp;&nbsp;         | 0 | 0 | 1 | 0 |
| **Combine with OR**&nbsp;&nbsp; | 1 | 0 | 1 | 0 |

El nuevo valor contiene ambos valores del enumerado en una sola variable

## Verificacion de valores

Luego de tener una variable con ambos valores, la pregunta es como podemos saber que valores contiene.

Esto lo podemos saber usando el operador de bits AND

| &nbsp;       | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
|-----------------|---|---|---|---|
| **bookingOptionsSelected**&nbsp;&nbsp;| 1 | 0 | 1 | 0 |
| **Breakfast**       | 1 | 0 | 0 | 0 |
| **resultado op AND** | 1 | 0 | 0 | 0 |

la operacion es la siguiente:

1. Tenemos la variable "bookingOptionsSelected" con los dos valores del enumerado
2. Tenemos el valor que queremos verificar ("Breakfast") que se encuentre dentro de la variable
3. Si el valor resultante de aplicar el operador AND entre el valor de la variable y el valor a verificar es igual al valor a verificar entonces la variable "bookingOptionsSelected" si contiene el valor Breakfast

la verificacion en c#:

```csharp
if ((bookingOptionsSelected & BookingOptions.Breakfast) != 0)
{
  //....
}
```
