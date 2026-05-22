# Parte 1: TAD Diccionario con T. Hash

En esta primera parte, realizaremos la implementaremos de un **Tipo Abstracto de Datos (TAD) Diccionario mediante una tabla&#x20;**_**hash**_. Este Diccionario permanente acceder a una colección de elementos mediante el uso de claves de acceso, trabajando con lo que comúnmente llamamos **pares&#x20;**_**clave→valor**_. La **clave será un tipo&#x20;**_**string**_ mientras que el valor será de tipo paramétrico, concretándose cuando se cree un objeto Diccionario.

<figure><img src="../.gitbook/assets/Gemini_Generated_Image_wgukbmwgukbmwguk.png" alt="" width="563"><figcaption><p>Diccionario con valores <code>float</code> y Diccionario con valores <code>int</code></p></figcaption></figure>

**Las tablas hash son extremadamente eficientes** pues en el mejor caso y en el caso medio todas las operaciones tienen un coste asintótico constante $$O(1)$$. Sin embargo, cuando la ocupación de la tabla es elevada, la probabilidad de colisión de claves es alta y el coste asintótico degenera hasta una función lineal $$O(n)$$.

Internamente, **una tabla&#x20;**_**hash**_**&#x20;es un array cuyos elementos denominamos cubetas**. Las cubetas pueden contener, o bien una entrada clave→valor, o bien un puntero a otra estructura de datos que es la que efectivamente almacena las entradas pertenecientes a dicha cubeta (p.e. una lista enlazada). Dada una entrada clave→valor, **se aplica una función&#x20;**_**hash**_**&#x20;a la clave que devuelve el identificador de la cubeta** (su posición en el vector de cubetas) en la que se debería encontrar o añadir dicho elemento.

En el caso de existir **colisiones de claves** (dos claves distintas reciben el mismo identificador de cubeta), existen diferentes métodos de resolución. En las sesiones de teoría se han tratado los métodos de encadenamiento y de direccionamiento directo. En el primer caso, las entradas se almacenan secuencialmente en una lista dinámica dentro de la cubeta correspondiente, mientras que en el segundo, las entradas se reubican aplicando una nueva función _hash_ dependiente del número de colisiones previas. **En esta práctica implementaremos el método de encadenamiento para resolver colisiones.**

<figure><img src="../.gitbook/assets/https___content.gitbook.com_content_UNn7pHmS3yDRrKDzSzAC_blobs_PlqgVUtgp2fsPf2Ayqim_image%20(3).avif" alt=""><figcaption></figcaption></figure>
