# Clase BSTreeDict\<V>

La interfaz [**Dict\<V>**](../parte-1-tad-diccionario-con-t.-hash/interfaz-dict-less-than-v-greater-than.md)**,** que en la primera parte de esta práctica se implementó con una tabla _hash (_&#x76;er clase [**`HashTable<V>`**](../parte-1-tad-diccionario-con-t.-hash/clase-hashtable-less-than-v-greater-than.md)), puede ser implementada igualmente mediante un ABB, representado por la clase [**BSTree\<T>**](clase-bstree-less-than-t-greater-than.md), que almacene elementos clave->valor de tipo [**TableEntry\<V>**](../parte-1-tad-diccionario-con-t.-hash/clase-tableentry-less-than-v-greater-than.md).&#x20;

En otras palabras, construiremos un objeto [**`BSTree<T>`**](clase-bstree-less-than-t-greater-than.md) cuyo tipo paramétrico `T` será [**`TableEntry<V>`**](../parte-1-tad-diccionario-con-t.-hash/clase-tableentry-less-than-v-greater-than.md) (`BSTree<TableEntry<V>>`). La clase genérica que implementará un diccionario con un ABB se denominará **`BSTreeDict<V>`**.

Las operaciones de la interfaz [**`Dict<V>`**](../parte-1-tad-diccionario-con-t.-hash/interfaz-dict-less-than-v-greater-than.md) serán delegadas a las operaciones correspondientes de la clase [**`BSTree<T>`**](clase-bstree-less-than-t-greater-than.md). Es por ello que la clase **`BSTreeDict<V>`** se puede considerar una especie de _**proxy**_ entre la interfaz [**`Dict<V>`**](../parte-1-tad-diccionario-con-t.-hash/interfaz-dict-less-than-v-greater-than.md) y la clase [**`BSTree<T>`**](clase-bstree-less-than-t-greater-than.md) que soportará la gestión de los elementos del diccionario.

{% hint style="warning" %}
Nota importante: **deberemos modificar la clase** [**`TableEntry<V>`**](../parte-1-tad-diccionario-con-t.-hash/clase-tableentry-less-than-v-greater-than.md) para incorporar la **sobrecarga de operadores `<` y `>`**. Esto permitirá comparar el orden de los objetos de dicha clase y buscar las posiciones en el ABB de dichos elementos.
{% endhint %}

## Atributos

<table><thead><tr><th width="149">Visibilidad</th><th width="290">Atributo</th><th>Descripción</th></tr></thead><tbody><tr><td><code>private</code></td><td><code>BSTree&#x3C;TableEntry&#x3C;V>>* tree</code> </td><td>ABB con elementos de tipo <code>TableEntry&#x3C;V></code> para gestionar los elementos de un diccionario.</td></tr></tbody></table>

## **Métodos**

<mark style="background-color:orange;">**Además de implementar los métodos públicos abstractos heredados de la interfaz**</mark> [<mark style="background-color:orange;">**`Dict<V>`**</mark>](../parte-1-tad-diccionario-con-t.-hash/interfaz-dict-less-than-v-greater-than.md), deberá definir e implementar los siguientes métodos propios:

<table><thead><tr><th width="127">Visibilidad</th><th width="286">Método</th><th>Descripción</th></tr></thead><tbody><tr><td><code>public</code></td><td><code>BSTreeDict()</code></td><td>Constructor. Crea un ABB vacío con memoria dinámica.</td></tr><tr><td><code>public</code></td><td><code>~BSTreeDict()</code></td><td>Método destructor. Se encargará de liberar la memoria dinámica ocupada por el ABB <code>tree</code>.</td></tr><tr><td><code>public</code></td><td><p><code>friend std::ostream&#x26; operator&#x3C;&#x3C;(</code></p><p>  <code>std::ostream &#x26;out,</code> </p><p>  <code>const BSTreeDict&#x3C;V> &#x26;bs)</code></p></td><td>Sobrecarga global del operador <code>&#x3C;&#x3C;</code> para imprimir el contenido del Diccionario por pantalla. </td></tr><tr><td><code>public</code></td><td><code>V operator[](std::string key)</code></td><td>Sobrecarga del operador<code>[]</code>. Actúa como interfaz al método de interfaz heredado <code>search(std::string key)</code>.</td></tr></tbody></table>

{% hint style="info" %}
Recuerda que la implementación de los métodos abstractos `entries()`,`insert()`, `search()` y `remove()` heredados de [**`Dict<V>`**](../parte-1-tad-diccionario-con-t.-hash/interfaz-dict-less-than-v-greater-than.md) harán uso de los métodos correspondientes de la clase [**`BSTree<T>`**](clase-bstree-less-than-t-greater-than.md) para gestionar las entradas clave->valor dentro de un ABB. Repasa brevemente su interfaz para tener claro como gestionar de forma eficaz esta sub-estructura de datos en el contexto de un ABB.
{% endhint %}

## Declaración e implementación de la clase BSTreeDict\<V>

Desde nuestro directorio de trabajo (raíz del repositorio git), abre Vim para crear el fichero `BSTreeDict.h` que contendrá tanto la definición como la implementación de la clase **`BSTreeDict<V>`**.

```bash
vim BSTreeDict.h
```

Escribe en él la declaración de la clase genérica **`BSTreeDict<V>`**, de acuerdo con la especificación del apartado anterior. A continuación tienes una "inicialización" o plantilla de dicho fichero, por si te sirve de ayuda para empezar:

```cpp
#ifndef BSTREEDICT_H
#define BSTREEDICT_H

#include <ostream>
#include <stdexcept>
#include "Dict.h"
#include "BSTree.h"
#include "TableEntry.h"

template <typename V>
class BSTreeDict: public Dict<V> {

    private:
        // ...

    public:
        // ...
        
};

#endif
```

&#x20;Guarda el fichero y, sin salir de vim, ejecuta el compilador g++ para depurar tu implementación:

```bash
:!g++ -c BSTreeDict.h  # Recuerda ejecutarlo desde el modo comando de vim!
```

Comprueba la salida del compilador. En casos de existir errores (seria lo más normal), examínalos con calma y detenimiento, y pulsa `ENTER` para volver al buffer de Vim para empezar a corregirlos. Repite este proceso, tantas veces como sea necesario, hasta que hayas depurado tu solución.&#x20;

&#x20;A continuación, añade el fichero al área de preparación de git:

```bash
git add BSTreeDict.h
```

y confirma los cambios con un mensaje informativo:

```bash
git commit -m "Añadida implementación de la clase BSTreeDict"
```

## Modificación de la clase TableEntry\<V>

Modifica la clase [**`TableEntry<V>`**](../parte-1-tad-diccionario-con-t.-hash/clase-tableentry-less-than-v-greater-than.md) para incorporar la **sobrecarga de operadores `<` y `>`**. Esto permitirá comparar el orden de los objetos de dicha clase y buscar las posiciones en el ABB de dichos elementos:

```cpp
friend bool operator<(const TableEntry<V> &te1, const TableEntry<V> &te2);
friend bool operator>(const TableEntry<V> &te1, const TableEntry<V> &te2);
```

Notad que la comparación `<` y `>` de objetos [**`TableEntry<V>`**](../parte-1-tad-diccionario-con-t.-hash/clase-tableentry-less-than-v-greater-than.md) se realizará por clave. Las claves son de tipo `std::string`, el cual ya implementa los operadores `<` y `>` aplicando un orden lexicográfico (el mismo que usan los diccionarios lingüísticos).&#x20;

## Depuración de la clase BSTreeDict\<V>

&#x20;Guarda en nuestro directorio de trabajo (`PRA_2425_P3`) el siguiente fichero para test:

{% file src="../.gitbook/assets/testBSTreeDict.cpp" %}

Examina su contenido. Verás que realiza una serie de operaciones en un Diccionario con valores enteros (el tipo `int` es paramétrico), a fin de testear las diferentes operaciones que nos brinda esta implementación.&#x20;

A continuación, procederemos a añadir al fichero `Makefile` una regla para generar el objetivo `bin/testBSTreeDict` (binario ejecutable). Este dependerá de los ficheros `Dict.h`, `BSTreeDict.h`, `BSNode.h` `TableEntry.h` y `testBSTreeDict.cpp`. &#x20;

```bash
vim Makefile
```

&#x20;Una vez implementada la regla, ejecútala:

```bash
make bin/testBSTreeDict
```

Finalmente, ejecuta el programa de test, para comprobar que tu implementación es correcta. Estando en el directorio raíz del proyecto:

```bash
./bin/testBSTreeDict
```

&#x20;Esto debería generar una salida parecida a esta:

<details>

<summary>Salida esperada del programa de test "testBSTreeDict"</summary>

```
Creating BSTreeDict<int> dict ...

dict.entries(): 0
cout << dict: 

dict.insert('c', 3) ...
dict.insert('f', 6) ...
dict.insert('a', 1) ...
dict.insert('b', 2) ...
dict.insert('d', 4) ...
dict.insert('e', 5) ...

cout << dict: 
('a' => 1) ('b' => 2) ('c' => 3) ('d' => 4) ('e' => 5) ('f' => 6) 

dict.search('a'): 1
dict['d']: 4
dict.remove('c'): 3

('a' => 1) ('b' => 2) ('d' => 4) ('e' => 5) ('f' => 6) 

dict.insert('a') => OK! throwed std::runtime_error: Duplicated element!
dict.search('j') => OK! throwed std::runtime_error: Element not found!
dict.remove('c') => OK! throwed std::runtime_error: Element not found!
```

</details>

&#x20;Si la semántica de tu salida es diferente, revisa tu código.&#x20;

{% hint style="warning" %}
Si la ejecución del programa se queda "colgada", seguramente sea porque ha entrado en un bucle infinito. Pulsa `CTRL+C` para "matar" el proceso, y revisa los bucles de tu código.&#x20;
{% endhint %}

Añade `testBSTreeDict.cpp` y `Makefile` a git (y `BSTreeDict.h` también, si has hecho cambios):

```bash
git add testBSTreeDict.cpp Makefile BSTreeDict.h
```

y confirma los cambios con un mensaje informativo:

```bash
git commit -m "Actualizado Makefile y añadido código de test de la clase BSTreeDict"
```

Este parece ser un buen momento para sincronizar tu repositorio local con tu repositorio remoto de GitHub, para enviarle todos los cambios (_commits_) realizados localmente:

```bash
git push
```
