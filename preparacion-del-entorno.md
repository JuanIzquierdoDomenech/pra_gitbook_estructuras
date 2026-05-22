# Preparación del entorno

## Crea un repositorio remoto en GitHub&#x20;

Entra a tu cuenta de GitHub y **crea un repositorio público, vacío** (sin inicializar), con el siguiente nombre: `PRA_2526_P2`. Copia la URL que se muestra tras la confirmación.&#x20;

## Clona el repositorio en tu equipo

Abre una terminal _Bash_ de Linux, sitúate en el directorio donde quieras mantener organizados tus repositorios git de la asignatura (p.e. `/home/jsilvestre/UPV/PRA/Lab`), y **clona el repositorio**:

```bash
git clone URL  # Reemplaza URL por lo que corresponda.
```

Este comando clonará tu repositorio de GitHub en un directorio llamado `PRA_2425_P3`, que, como podrás comprobar, está vacío. Sitúate en ese directorio para "entrar" dentro de nuestro repositorio git local:

```bash
cd PRA_2425_P3
```

Este repositorio local está enlazado con el repositorio remoto de GitHub, por lo que los comandos `git pull` y `git push` interactuarán con él.&#x20;

{% hint style="warning" %}
Tened en cuenta que `PRA_2425_P3` será nuestro directorio de trabajo durante toda la práctica. Es decir, todos los ficheros se guardaran en ese directorio, y todos los comandos se ejecutarán desde ese directorio.
{% endhint %}
