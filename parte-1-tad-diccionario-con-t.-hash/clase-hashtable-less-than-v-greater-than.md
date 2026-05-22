# Clase HashTable\<V>

Esta clase implementará la interfaz [**`Dict<V>`**](interfaz-dict-less-than-v-greater-than.md) mediante una **tabla hash con encadenamiento**. Más concretamente, la tabla hash se implementará como un array de punteros a listas de tipo **`ListLinked<T>`** (ver [Práctica 1](https://app.gitbook.com/o/uY9F7U6WRW2jZBN5gWuV/s/sfbBaRe5dlDS9ZlSiKn6/)). Para ello, tienes dos alternativas:

1. <mark style="background-color:green;">**(Preferible)**</mark> Hacer el `include` correspondiente hacia la ruta donde esté vuestro fichero `ListLinked.h`, p.e. **`#include "../PRA_2627_P1/ListLinked.h"`** (modificar de manera acorde).
2. <mark style="background-color:red;">**(Desaconsejable)**</mark> Copiar los ficheros `Node.h`, `List.h` y `ListLinked.h` a la ubicación de la Práctica 2 para que esté todo siempre disponible, y simplemente hacer **`#include "ListLinked.h"`**.

{% hint style="info" %}
Si por alguna razón vuestra clase **`ListLinked<T>`** no se ha implementado correctamente, podéis utilizar, de forma subóptima, la clase **`ListArray<T>`** de la [Práctica 1](https://app.gitbook.com/o/uY9F7U6WRW2jZBN5gWuV/s/sfbBaRe5dlDS9ZlSiKn6/), o bien la clase [**`std::list<T>`** ](https://cplusplus.com/reference/list/list/)de la librería estándar de C++, que también implementa una lista basada en secuencias nodos enlazados, pero con otra interfaz de método&#x73;_._
{% endhint %}

### Atributos

<table><thead><tr><th width="149">Visibilidad</th><th width="290">Atributo</th><th>Descripción</th></tr></thead><tbody><tr><td><code>private</code></td><td><code>int n</code></td><td>Número de elementos almacenados actualmente en la tabla hash.</td></tr><tr><td><code>private</code></td><td><code>int max</code></td><td>Tamaño de la tabla hash (número total de cubetas).</td></tr><tr><td><code>private</code></td><td><code>ListLinked&#x3C;TableEntry&#x3C;V>>* table</code></td><td>Tabla de cubetas, representada por un array de punteros a listas enlazadas (tipo <strong><code>ListLinked&#x3C;T></code></strong>) que almacenan pares clave→valor (tipo <a href="clase-tableentry-less-than-v-greater-than.md"><strong><code>TableEntry&#x3C;V></code></strong></a>).</td></tr></tbody></table>

### **Métodos**

<mark style="background-color:orange;">**Además de implementar los métodos públicos heredados de la interfaz**</mark> [<mark style="background-color:orange;">**`Dict<V>`**</mark>](interfaz-dict-less-than-v-greater-than.md), deberá definir e implementar los siguientes métodos propios:

<table><thead><tr><th width="127">Visibilidad</th><th width="286">Método</th><th>Descripción</th></tr></thead><tbody><tr><td><code>private</code></td><td><code>int h(std::string key)</code></td><td>Función <em>hash</em> que devuelve la posición (cubeta) en la tabla <em>hash</em> de <strong>key</strong>.  Se calculará como el resto de la divisón entre la suma de los valores ASCII numéricos de los caracteres de la clave y el tamaño de la tabla <em>hash</em> (ver nota más abajo).</td></tr><tr><td><code>public</code></td><td><code>HashTable(int size)</code></td><td>Método constructor. Reservará memoria dinámica para crear una tabla <code>table</code> de tamaño <strong>size</strong>, e inicializará los atributos <code>n</code> y <code>max</code> de la clase.</td></tr><tr><td><code>public</code></td><td><code>~HashTable()</code></td><td>Método destructor. Se encargará de liberar la memoria dinámica reservada al crear la tabla <code>table</code>.</td></tr><tr><td><code>public</code></td><td><code>int capacity()</code></td><td>Devuelve el número total de cubetas de la tabla.</td></tr><tr><td><code>public</code></td><td><code>friend std::ostream&#x26; operator&#x3C;&#x3C;(std::ostream &#x26;out, const HashTable&#x3C;V> &#x26;th)</code></td><td>Sobrecarga global del operador <code>&#x3C;&#x3C;</code> para imprimir el contenido de la tabla <em>hash</em> por pantalla. Recuerda incluir la cabecera <code>&#x3C;ostream></code> en el <code>.h</code>.</td></tr><tr><td><code>public</code></td><td><code>V operator[](std::string key)</code></td><td>Sobrecarga del operador <code>[]</code>. Devuelve el valor correspondiente a <strong>key</strong>. Si no existe, lanza la excepción <strong><code>std::runtime_error</code></strong>.</td></tr></tbody></table>

{% hint style="success" %}
El método `at(i)` de `std::string` permite obtener el carácter situado en la posición `i` de un `string`, y `int(c)` permite obtener el valor ASCII numérico del carácter `c`.
{% endhint %}

{% hint style="info" %}
Recuerda que los métodos `insert()`, `search()` y `remove()` de esta clase harán uso de los métodos de la interfaz **`List<T>`** implementados por **ListLinked\<T>** para gestionar las entradas clave->valor de cada cubeta. Repasa brevemente su interfaz para tener claro como gestionar de forma eficaz esta sub-estructura de datos en el contexto de una tabla hash.\
\
En particular, debes ser consciente de que la operación de buscar una entrada clave->valor en una **`List<T>`** implicará buscar la existencia en dicha lista de un **`TableEntry<V>`** con la clave correspondiente.
{% endhint %}

## Declaración e implementación de la clase HashTable\<V>

Desde nuestro directorio de trabajo (raíz del repositorio git), abre Vim para crear el fichero `HashTable.h` que contendrá tanto la definición como la implementación de la clase `HashTable<V>`.

```bash
vim HashTable.h
```

Escribe en él la declaración de la clase genérica `HashTable<V>`, de acuerdo con la especificación del apartado anterior. A continuación tienes una "inicialización" o plantilla de dicho fichero, por si te sirve de ayuda para empezar <mark style="background-color:orange;">(recuerda modificar el include de</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`ListLinked.h`</mark><mark style="background-color:orange;">):</mark>

```cpp
#ifndef HASHTABLE_H
#define HASHTABLE_H

#include <ostream>
#include <stdexcept>
#include "Dict.h"
#include "TableEntry.h"

#include "../PRA_2627_P1/ListLinked.h"  // ¡ADAPTA A TU RUTA!

template <typename V>
class HashTable: public Dict<V> {

    private:
        // ...

    public:
        // ...
        
};

#endif
```

&#x20;Guarda el fichero y, sin salir de vim, ejecuta el compilador g++ para depurar tu implementación:

```bash
:!g++ -c HashTable.h  # Recuerda ejecutarlo desde el modo comando de vim!
```

Comprueba la salida del compilador. En casos de existir errores (seria lo más normal), examínalos con calma y detenimiento, y pulsa `ENTER` para volver al buffer de Vim para empezar a corregirlos. Repite este proceso, tantas veces como sea necesario, hasta que hayas depurado tu solución.&#x20;

&#x20;A continuación, añade el fichero al área de preparación de git:

```bash
git add TablaHash.h
```

y confirma los cambios con un mensaje informativo:

```bash
git commit -m "Añadida implementación de la clase HashTable"
```

## Depuración de la clase HashTable\<V>

&#x20;Guarda en nuestro directorio de trabajo (`PRA_2425_P3`) el siguiente fichero para test:

{% file src="../.gitbook/assets/testHashTable.cpp" %}

Examina su contenido. Verás que realiza una serie de operaciones en un Diccionario con valores enteros (el tipo `int` es paramétrico), a fin de testear las diferentes operaciones que nos brinda esta implementación.&#x20;

A continuación, procederemos a añadir al fichero `Makefile` una regla para generar el objetivo `bin/testHashTable` (binario ejecutable). Este dependerá de los ficheros `Dict.h`, `HashTable.h`, `TableEntry.h` y `testHashTable.cpp`. &#x20;

```bash
vim Makefile
```

&#x20;Una vez implementada la regla, ejecútala:

```bash
make bin/testHashTable
```

Finalmente, ejecuta el programa de test, para comprobar que tu implementación es correcta. Estando en el directorio raíz del proyecto:

```bash
./bin/testHashTable
```

&#x20;Esto debería generar una salida parecida a esta:

<details>

<summary>Salida esperada del programa de test "testHashTable"</summary>

```
HashTable [entries: 0, capacity: 3]
==============

== Cubeta 0 ==

List => []

== Cubeta 1 ==

List => []

== Cubeta 2 ==

List => []

==============

dict.capacity(): 3
dict.entries(): 0

dict.insert('One', 1) ...
dict.insert('Two', 2) ...
dict.insert('Three', 3) ...
dict.insert('Four', 4) ...
dict.insert('Five', 5) ...
dict.insert('Six', 6) ...


HashTable [entries: 6, capacity: 3]
==============

== Cubeta 0 ==

List => [
  ('Three' => 3)
]

== Cubeta 1 ==

List => [
  ('Five' => 5)
  ('Four' => 4)
]

== Cubeta 2 ==

List => [
  ('Six' => 6)
  ('Two' => 2)
  ('One' => 1)
]

==============

dict.search('One'): 1
dict['Four']: 4
dict.remove('Three'): 3


HashTable [entries: 5, capacity: 3]
==============

== Cubeta 0 ==

List => []

== Cubeta 1 ==

List => [
  ('Five' => 5)
  ('Four' => 4)
]

== Cubeta 2 ==

List => [
  ('Six' => 6)
  ('Two' => 2)
  ('One' => 1)
]

==============

dict.insert('One') => throwed std::runtime_error: Key 'One' already exists!
dict.search('Ten') => throwed std::runtime_error: Key 'Ten' not found!
dict.remove('Ten') => throwed std::runtime_error: Key 'Ten' not found!
```

</details>

&#x20;Si tu salida es diferente, revisa tu código.&#x20;

{% hint style="danger" %}
Si detectas que en tu implementación los pares clave->valor no se guardan en las mismas cubetas que en la salida esperada, revisa la función hash `h(std::string key)`.
{% endhint %}

{% hint style="warning" %}
Si la ejecución del programa se queda "colgada", seguramente sea porque ha entrado en un bucle infinito. Pulsa `CTRL+C` para "matar" el proceso, y revisa los bucles de tu código.&#x20;
{% endhint %}

{% hint style="success" %}
Puedes modificar el código de test para crear una tabla _hash_ mayor y añadir más pares para comprobar el rendimiento de la función _hash_.&#x20;
{% endhint %}

Añade `testHashTable.cpp` y `Makefile` a git (y `HashTable.h` también, si has hecho cambios):

```bash
git add testHashTable.cpp Makefile HashTable.h
```

y confirma los cambios con un mensaje informativo:

```bash
git commit -m "Actualizado Makefile y añadido código de test de la clase HashTable"
```

Este parece ser un buen momento para sincronizar tu repositorio local con tu repositorio remoto de GitHub, para enviarle todos los cambios (_commits_) realizados localmente:

```bash
git push
```
