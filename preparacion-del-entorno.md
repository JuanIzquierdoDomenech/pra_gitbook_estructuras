---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Preparación del entorno

## Crea un repositorio remoto en GitHub&#x20;

Entra a tu cuenta de GitHub y **crea un repositorio público, vacío** (sin inicializar), con el siguiente nombre: `PRA_2627_P2`. Copia la URL que se muestra tras la confirmación.&#x20;

## Clona el repositorio en tu equipo

Abre una terminal _Bash_ de Linux, sitúate en el directorio donde quieras mantener organizados tus repositorios git de la asignatura (p.e. `/home/TUUSUARIO/UPV/PRA/Lab`), y **clona el repositorio**:

```bash
git clone ${URL}  # Reemplaza {URL} por lo que corresponda.
```

Este comando clonará tu repositorio de GitHub en un directorio llamado `PRA_2627_P2`, que, como podrás comprobar, está vacío. Sitúate en ese directorio para "entrar" dentro de nuestro repositorio git local:

```bash
cd PRA_2627_P2
```

Este repositorio local está enlazado con el repositorio remoto de GitHub, por lo que los comandos `git pull` y `git push` interactuarán con él.&#x20;

{% hint style="warning" %}
Tened en cuenta que `PRA_2627_P2` será nuestro directorio de trabajo durante toda la práctica. Es decir, todos los ficheros se guardaran en ese directorio, y todos los comandos se ejecutarán desde ese directorio.
{% endhint %}

***

### Fichero .gitignore

Recuerda añadir el fichero .gitignore a tu repositorio, de manera similar a la P1.

{% code title="" %}
```bash
# Prerequisites
*.d

# Compiled Object files
*.slo
*.lo
*.o
*.obj

# Precompiled Headers
*.gch
*.pch

# Linker files
*.ilk

# Debugger Files
*.pdb

# Compiled Dynamic libraries
*.so
*.dylib
*.dll
*.so.*

# Fortran module files
*.mod
*.smod

# Compiled Static libraries
*.lai
*.la
*.a
*.lib

# Executables
*.exe
*.out
*.app

# Build directories
build/
Build/
build-*/
bin/

# CMake generated files
CMakeFiles/
CMakeCache.txt
cmake_install.cmake
Makefile
install_manifest.txt
compile_commands.json

# Temporary files
*.tmp
*.log
*.bak
*.swp

# vcpkg
vcpkg_installed/

# debug information files
*.dwo

# test output & cache
Testing/
.cache/

# MacOS
.DS_Store


```
{% endcode %}
