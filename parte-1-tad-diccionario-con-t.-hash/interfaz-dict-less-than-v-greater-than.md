# Interfaz Dict\<V>

La interfaz genérica `Dict<V>`determinará de qué manera se puede gestionar un Diccionario de pares clave→valor, donde clave será de tipo _string_ y valor de tipo `V` cualquiera. `Dict<V>` será una **clase abstracta pura y genérica** (templatizada), e incluirá los siguientes métodos **virtuales puros y genéricos**:

| Método                                      | Descripción                                                                                                                                                                         |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`void insert(std::string key, V value)`** | Inserta el par **key**->**value** en el diccionario. Lanza una excepción **`std::runtime_error`** si **`key`** ya existe en el diccionario.                                         |
| **`V search(std::string key)`**             | Busca el valor correspondiente a **key**. Devuelve el valor **value** asociado si **key** está en el diccionario. Si no se encuentra, lanza una excepción **`std::runtime_error`**. |
| **`V remove(std::string key)`**             | Elimina el par **key**->**value** si se encuentra en el diccionario. Si no se encuentra, lanza una excepción **`std::runtime_error`**.                                              |
| **`int entries()`**                         | Devuelve el número de elementos que tiene el Diccionario.                                                                                                                           |

## Declaración de la interfaz Dict\<V>

Desde nuestro directorio de trabajo (`PRA_2425_P3`, raíz del repositorio git), abre vim para crear el fichero de cabeceras `Dict.h`:

```bash
vim Dict.h
```

Declara en él la clase abstracta pura `Dict`, de acuerdo con la especificación de la tabla del apartado anterior. &#x20;

Por si en un futuro la clase fuese importada desde múltiples fuentes, **podemos envolver la definición de la clase dentro de una guarda de importación** _("include guard")_, usando las directivas del preprocesador `ifndef <VAR>` _(if-not-defined)_ y `define <VAR>`. Esto nos evitará los errores de compilación correspondientes a una importación múltiple. Aquí tienes una plantilla:

```cpp
#ifndef DICT_H
#define DICT_H
#include <string>

template <typename V> 
class Dict {
    public:
        // ... aquí los métodos virtuales puros
};

#endif
```

Guarda el fichero y ejecuta `g++` en modo comprobación de sintaxis (opción `-fsyntax-only`) para asegurarnos que no hemos cometido ningún error en la declaración:

```bash
g++ -fsyntax-only Dict.h
```

{% hint style="success" %}
Recuerda que puedes ejecutar este comando (y cualquier otro) sin salir de vim. Estando en modo comando, teclea **`:!`**&#x73;eguido del comando que desees ejecutar. En este caso:

```bash
:!g++ -fsyntax-only Dict.h
```
{% endhint %}

A continuación, añade el fichero al área de preparación de git:

```bash
git add Dict.h
```

y confirma los cambios con un mensaje informativo:

```bash
git commit -m "Añadida interfaz genérica Dict"
```

&#x20;Si lo crees conveniente, haz `git push` para enviar los cambios a tu repositorio remoto en GitHub.&#x20;

{% hint style="info" %}
Cuando hagas `git push`, te pedirá tu usuario y contraseña en GitHub.&#x20;

Recuerda que debes introducir tu **token de acceso personal**, y no tu contraseña de acceso web! Asegúrate que tu token aún es válido (podría haber caducado; en ese caso, genera uno nuevo).

Una alternativa es generar un par [clave pública/privada SSH](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) en tu máquina habitual de trabajo (solo si es tu equipo personal, no si es equipo del laboratorio) para que el repositorio 'confié' en tu máquina.
{% endhint %}
