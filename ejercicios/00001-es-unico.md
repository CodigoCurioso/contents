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

#### ¿Qué codificación se utilizará?

Cuando un ejercicio de programación hace uso de caracteres puede ser importante conocer el tipo de codificación que se utilizará. Si sabes el tipo de codificación a utilizar te dará la posibilidad de realizar algoritmos más eficientes.

No es lo mismo esperar recibir una cadena de texto ASCII a recibir una cadena de texto Unicode. ASCII está compuesto de 128 carateres mientras que Unicode actualmente en la versión 13.0 tiene 143924 caracteres, una diferencia considerable. Por otro lado ASCII extendido cuenta con 256 caracteres.

Si en el enunciado del problema no especifica la codificación, puedes preguntarle al entrevistador si sabe el tipo de codificación a utilzar. Si te dice la codificación ya tienes un dato importante para definir tu algoritmo, si no al menos mostraste al entrevistador que prestas atención a los detalles ;)

#### Retornar una respuesta rápidamente en cadenas de texto largas

Si se te ha dado la codificación, éste puede ser utilizado para determinar si hay caracteres duplicados en cadenas de texto largas rápidamente.

Supongamos que se te ha dicho que la cadena de texto que recibirá el algoritmo es ASCII. Habíamos mencionado que ASCII se compone de 128 caracteres únicos, entonces es válido suponer que si una cadena de texto tiene una longitud de 129 al menos un caracter está duplicado. En ASCII no es posible tener cadenas de texto de longitud mayor a 128 sin que haya al menos un caracter duplicado.

Este es un punto importante a considerar ya que ayuda a crear un algoritmo altamente eficiente. Se puede definir una condición que valida la longitud de la cadena de texto. Si la cadena de texto es mayor a 128 caracteres se devuelve false inmediatamente. Si no, se recorre todo la cadena de texto en busca de duplicados, pero en el peor de los casos se recorrerá una cadena de texto de 128 caracteres.

Dado lo anterior, puedes utilizar esta condición en tu código:

``` JavaScript
if (text.length > 128) {
    return false;
}
```

#### Almacenamiento en memoria

En este ejercicio necesitarás almacenar temporalmente en memoria los caracteres revisados.

Debes conocer bien el lenguaje utilizado para determinar la mejor estructura a utilizar. Es importante considerar que debes poder almacenar la letra revisada, pero además deberás de poder buscarlo rápidamente si la nacesitas.

Opciones para almacenar en estos casos están las **tablas hash** o **diccionarios**. También puedes considerar utilizar un **arreglo indexado**.

Si optas por utilizar un arreglo y el lenguaje necesita que definas la longitud, puedes definirlo conociendo el tipo de codificación.

``` Java
boolean[] lettersFound = new boolean[128];
```

Independiente del almacenamiento utilizado, toma encuenta almacenar la menor información posible. Si necesitas definir un tipo de dato, procura utilizar boleanos o bit.

### Respuestas

#### Respuesta 1

Si no sabes la codificación de texto puedes crear un código como el siguiente (Entre más largo el texto más iteraciones tendrá que realizar).

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

Si sabes que la codificación es ASCII puedes utilizar el siguiente código (En textos mayores a 128 caracteres devolverá el resultado inmediatamente).

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

Si no es permitido utilizar estructuras de datos adicionales, deberás de utilizar dos ciclos.

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

Si te es permitido modificar el string de entrada, podrías ordenarlo primero y verificar si hay dos letras a la par iguales.

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
