# Clase TableEntry\<V>

Los **pares clave→valor** se representarán mediante la clase genérica `TableEntry<V>`, con tipo `std::string` para las claves y tipo paramétrico `V` para los valores.&#x20;

### Atributos

<table><thead><tr><th width="149">Visibilidad</th><th width="190">Atributo</th><th>Descripción</th></tr></thead><tbody><tr><td><code>public</code></td><td><code>std::string key</code></td><td>El elemento clave del par. </td></tr><tr><td><code>public</code></td><td><code>V value</code></td><td>El elemento valor del par.</td></tr></tbody></table>

### Métodos

Conviene sobrecargar los operadores `==` y `!=` para determinar que los pares clave->valor representados por `TableEntry<V>` se comparan solo usando la clave. Esto nos servirá para detectar colisiones de claves en la posterior implementación&#x20;

<table><thead><tr><th width="127">Visibilidad</th><th width="255">Método</th><th>Descripción</th></tr></thead><tbody><tr><td><code>public</code></td><td><code>TableEntry(std::string key, V value)</code></td><td>Método constructor con el par clave->valor.</td></tr><tr><td><code>public</code></td><td><code>TableEntry(std::string key)</code></td><td>Crea una entrada solo con clave (sin valor). </td></tr><tr><td><code>public</code></td><td><code>TableEntry()</code></td><td>Crea una entrada con la clave <code>""</code> (cadena vacía) y sin valor.</td></tr><tr><td><code>public</code></td><td><code>friend bool operator==(const TableEntry&#x3C;V> &#x26;te1, const TableEntry&#x3C;V> &#x26;te2)</code></td><td>Sobrecarga global del operador <code>==</code> para determinar que dos instancias de TableEntry son iguales solo si comparten la misma clave (con independencia del valor).</td></tr><tr><td><code>public</code></td><td><code>friend bool operator!=(const TableEntry&#x3C;V> &#x26;te1, const TableEntry&#x3C;V> &#x26;te2)</code></td><td>Sobrecarga global del operador <code>!=</code> para determinar que dos instancias de TableEntry son diferentes solo si sus claves son distintas (con independencia del valor).</td></tr><tr><td><code>public</code></td><td><code>friend std::ostream&#x26; operator&#x3C;&#x3C;(std::ostream &#x26;out, const TableEntry&#x3C;V> &#x26;te)</code></td><td>Sobrecarga global del operador <code>&#x3C;&#x3C;</code> para imprimir el contenido de la entrada (par clave->valor) por pantalla. Recuerda incluir la cabecera <code>&#x3C;ostream></code> en el <code>.h</code>.</td></tr></tbody></table>

## Declaración e implementación de la clase TableEntry\<V>

{% hint style="danger" %}
**La definición e implementación de clases genéricas/templatizadas se debe realizar en un único fichero de cabeceras (.h)**, para que el compilador pueda generar código específico derivado de los templates (más info [aquí](https://isocpp.org/wiki/faq/templates#templates-defn-vs-decl)).
{% endhint %}

Desde nuestro directorio de trabajo (raíz del repositorio git), abre Vim para crear el fichero `TableEntry.h` que contendrá tanto la definición como la implementación de la clase `TableEntry<V>`.

```bash
vim TableEntry.h
```

Escribe en él la declaración de la clase genérica `TableEntry<V>`, de acuerdo con la especificación del apartado anterior. A continuación tienes una "inicialización" o plantilla de dicho fichero, por si te sirve de ayuda para empezar:

```cpp
#ifndef TABLEENTRY_H
#define TABLEENTRY_H

#include <string>
#include <ostream>

template <typename V> 
class TableEntry {
    public:
        // miembros públicos
    
};

#endif
```

Guarda el fichero y, sin salir de vim, ejecuta el compilador g++ para depurar tu implementación:

```bash
:!g++ -c TableEntry.h  # Recuerda ejecutarlo desde el modo comando de vim!
```

Comprueba la salida del compilador, y depura tu implementación en caso necesario.  A continuación, añade el fichero al área de preparación de git:

```bash
git add TableEntry.h
```

y confirma los cambios con un mensaje informativo:

```bash
git commit -m "Añadida implementación de la clase TableEntry"
```

Si lo crees conveniente, haz `git push` para enviar los cambios a tu repositorio remoto en GitHub.&#x20;

## Depuración de la clase TableEntry\<V>

&#x20;Guarda en nuestro directorio de trabajo (`PRA_2425_P3`) el siguiente fichero para test:

{% file src="../.gitbook/assets/testTableEntry.cpp" %}

Examina su contenido. Verás que realiza una serie de operaciones diferentes instancias de `TableEntry` con `V=int`, a fin de testear los operadores sobrecargados.&#x20;

{% hint style="info" %}
Fíjate que, al importar el fichero `TableEntry.h,`no solo se importa la definición (interfaz) de la clase, sino también su implementación. Esto resulta imprescindible en clases templatizadas, ya que el compilador necesita conocer tanto la implementación de la plantilla como los tipos concretos (int, double, string, etc.) que "rellenarán" dicha plantilla, a fin de generar el código específico a ser ejecutado.
{% endhint %}

A continuación, procederemos a inicializar el fichero `Makefile` para automatizar el proceso de compilación del proyecto. En esta primera fase, implementaremos dos reglas:

* Una regla para generar el objetivo `bin/testTableEntry` (binario ejecutable). Este dependerá de  `TableEntry.h`y `testTableEntry.cpp`. &#x20;
* Una regla `clean` que elimine todos los archivos `.o` y `.gch` generados en el directorio, así como el subdirectorio `bin`.&#x20;

{% hint style="info" %}
Para una mejor organización, los ficheros binarios ejecutables del proyecto se generaran en un subdirectorio denominado **`bin`**.
{% endhint %}

&#x20;Estando en el directorio raíz del proyecto, abre vim para crear el fichero `Makefile`:

```bash
vim Makefile
```

y añade las dos reglas:

```makefile
bin/testTableEntry: testTableEntry.cpp TableEntry.h
        mkdir -p bin
        g++ -o bin/testTableEntry testTableEntry.cpp

clean:
        rm -rf *.o *.gch bin
```

{% hint style="warning" %}
Recuerda: **debes usar tabulador** (tecla `TAB`) para indentar los comandos de la regla.
{% endhint %}

A continuación, ejecuta la regla `bin/testHashTable`:

```bash
make bin/testTableEntry
```

Finalmente, ejecuta el programa de test, para comprobar que tu implementación es correcta. Estando en el directorio raíz del proyecto:

```bash
./bin/testTableEntry
```

&#x20;Esto debería generar una salida parecida a esta:

<details>

<summary>Salida esperada del programa de test "testTableEntry"</summary>

```
e1: ('Catorze' => 14)
e2: ('Trenta-tres' => 33)
e3: ('Trenta-tres' => 123)

e1 == e2 ? false
e1 != e2 ? true

e1 == e3 ? false
e1 != e3 ? true

e2 == e3 ? true
e2 != e3 ? false
```

</details>

&#x20;Si tu salida es diferente, revisa tu código.&#x20;

Añade `testTableEntry.cpp` y `Makefile` a git (y `TableEntry.h` también, si has hecho cambios):

```bash
git add testTableEntry.cpp Makefile TableEntry.h
```

y confirma los cambios con un mensaje informativo:

```bash
git commit -m "Añadido Makefile y código de test de la clase TableEntry"
```

Este parece ser un buen momento para sincronizar tu repositorio local con tu repositorio remoto de GitHub, para enviarle todos los cambios (_commits_) realizados localmente:

```bash
git push
```
