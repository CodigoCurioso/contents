---
id: 00001
category: ejercicio
title: "¿Es Único?"
description: "Determinar si una cadena de texto tiene caracteres duplicados"
tags: caracteres cadena-de-texto duplicados arreglos
difficulty: 1
content: https://github.com/CodigoCurioso/contents/blob/main/ejercicios/00001-es-unico.md
date: 2020-11-04
---

# ¿Es Único?

## Descripción

Implemente un algoritmo para determinar si una cadena de texto tiene sólo caracteres únicos.

### Resultados esperados

``` shell
 > IsUnique("abcd");
   true
```

``` shell
 > IsUnique("abccd");
   false
```

## Solución

### Análisis

#### Codificación

Cuando un ejercicio de programación hace uso de caracteres puede ser importante conocer el tipo de codificación que utilizará. Conociendo el tipo de codificación te dará la posibilidad de realizar mejores algoritmos.

Por ejemplo, ASCII y Unicode son codificaciones que varian en la cantidad de caracteres soportados. ASCII está compuesto de 128 carateres mientras que Unicode en la versión 13.0 tiene 143 924 caracteres, una diferencia considerable.

> ASCII está compuesto de 128 caracteres, Unicode 143 924

Si estás en una entrevista de trabajo y el enunciado no especifica la codificación, puedes preguntarle al entrevistador si sabe el tipo de codificación a utilzar. Si te dice la codificación ya tienes un dato importante para definir tu algoritmo, si no al menos mostraste al entrevistador que prestas atención a los detalles ;)

#### Utilizando la codificación en el algoritmo

Si se te ha dado una codificación es importante que lo utilices de manera adecuada en tu algoritmo.

Supongamos que se te ha dicho que la cadena de texto que recibirá el algoritmo es ASCII. Habíamos mencionado anteriormente que ASCII se compone de 128 caracteres únicos, entonces es válido suponer que si una cadena de texto tiene una longitud de 129 tendrá al menos un caracter duplicado.

> En ASCII no es posible tener cadenas de texto de longitud mayor a 128 sin que haya al menos un caracter duplicado.

Este es un punto importante a considerar ya que ayuda a crear un algoritmo altamente eficiente. Se puede definir una condición que valida la longitud de la cadena de texto. Si la cadena de texto es mayor a 128 caracteres se devuelve false inmediatamente. Si no, se recorre todo la cadena de texto en busca de duplicados, pero en el peor de los casos se recorrerá una cadena de texto de 128 caracteres.

Dado lo anterior, puedes utilizar esta condición en tu código:

``` JavaScript
if (text.length > 128) {
    return false;
}
```

#### Almacenamiento en memoria

En este ejercicio necesitarás almacenar temporalmente en memoria los caracteres revisados, dependiendo del lenguaje tendrás diferentes opciones.

Considera utilizar una estructura de datos que no ocupe mucho espacio en memoria y puedas obtener sus valores rápidamente. Algunas opciones son las **tablas hash**,  **diccionarios** o **arreglos indexados**.

Si optas por utilizar un arreglo y el lenguaje necesita que definas su longitud, recuerda que la coficación te ayudará a definirlo.

``` Java
boolean[] lettersFound = new boolean[128]; // Codificación ASCII: 128 caracteres
```

Procura almacenar valores que no ocupen mucho espacio en memoria. Puedes utilizar **booleanos** o **bit**.

### Respuestas

#### Respuesta 1

Si no sabes la codificación de texto, tendrás que hacer un recorrido de todas las letras del texto hasta encontrar una letra ya revisada anteriormente. Este código tiene el inconveniente que entre más largo el texto igualmente aumentarán las iteraciones que tendrá que realizar.

``` JavaScript
function IsUnique(text) {
    let result = true;
    const lettersFound = [];

    for(letter of text) {
        if (lettersFound[letter]) {
            result = false;
            break;
        }

        lettersFound[letter] = true;
    }

    return result;
}
```

#### Respuesta 2

Si sabes la codificación, puedes utilizarla a tu favor. Esta respuesta muestra una solucion utilizando ASCII. Tiene la ventaja de que en textos mayores a 128 caracteres devolverá el resultado `false` sin realizar el ciclo.

``` JavaScript
const ASCII_LENGTH = 128;

function IsUnique(text) {
    let result = true;
    const lettersFound = [];

    if (text.length > ASCII_LENGTH) {
        result = false;
    } else {
        for(letter of text) {
            if (lettersFound[letter]) {
                result = false;
                break;
            }

            lettersFound[letter] = true;
        }
    }

    return result;
}
```

#### Respuesta 3

Si el enunciado no te permite utilizar estructuras de datos adicionales, tendrás que crear dos ciclos en busca de la letra duplicada.

``` JavaScript
function IsUnique(text) {

    for(let i = 0; i < text.length; i++) {
      for(let j = i + 1; j < text.length; j++) {
        if (text[i] == text[j]) {
          return false;
        }
      }
    }

    return true;
}
```

#### Respuesta 4

Si te dicen que recibirás un texto ordenado o que tienes la posibilidad de ordenarlo, sólo tendrás que revisar si hay dos letras iguales a la par. El algoritmo sería así:

``` JavaScript
function IsUnique(text) {

    const sortedText = SortString(text);

    for(let i = 0; i < sortedText.length - 1; i++) {
      if (sortedText[i] == sortedText[i + 1]) {
        return false;
      }
    }

    return true;
}
```
