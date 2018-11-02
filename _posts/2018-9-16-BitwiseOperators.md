---
tags:
  - c#
  - bitwise operators
layout: post
title: 'C# Bitwise Operators'
category: c#
comments: true
---

# C# Bitwise Operators

Entender la manipulación de bits es util en escenario donde tenemos que usar menos cantidad de memoria para guardar datos

## Attributo Flag
El Attributo Flag permite el poder 


```csharp
[Flag]
public enum BookingOptions
{
  None = 0,
  EnSuite = 1,
  SeaView = 2,
  StairFreeAccess = 4,
  Breakfast = 8
}

```

## Configuración 

Una vez instalado el package podremos encontrar el ejecutable ilmerge.exe dentro de la carpeta package, copiarlo dentro del directorio del proyecto

## Uso
Tenemos un proyecto de libreria de clases MyLibrary la cual usa StructureMap.dll , StructureMap.AutoMocking.dll y  Rhino.Mocks.dll, ejecutando la siguiente linea de comnandos se lograra unir todas las librerias en una sola dentro del directorio Deploy: MyLibrary.dll

```dosbatch
ILMerge.exe /t:library /out:'Deploy/MyLibrary.dll'
  'MyLibrary.dll'
  'StructureMap.dll'
  'StructureMap.AutoMocking.dll'
  'Rhino.Mocks.dll'
```
## Problemas comunes

Cuando distribuimos nuestra libreria puede ocurrir el siguiente problema, puede que en el proyecto donde se use nuestra dll también se este usando la misma libreria de un tercero que usamos previamente, lo cual originaria un problema de referencias en algunos casos, para resolver esto ilmerge provee el comando **internalize** para cambiar todos los metodos y clases **public** a **internal** y la posibilidad de excluir las dlls que querramos usando un archivo de texto

```dosbatch
ILMerge.exe /t:library /internalize:'Build/ILMergeIncludes.txt' /out:'Deploy/MyLibrary.dll'
  'MyLibrary.dll'
  'StructureMap.dll'
  'StructureMap.AutoMocking.dll'
  'Rhino.Mocks.dll'
```

ILMergeIncludes.txt:

```sh
StructureMap
StructureMap.AutoMocking
Rhino.Mocks
```	

De esta forma solo los metodos y clases de nuestra dll quedan públicas para ser usadas 
