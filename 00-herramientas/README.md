# Herramientas para las prácticas

#### Tabla de contenido

 * [git](#git)
 * [docker](#docker)
 * [qemu](#qemu)
 * [gcc](#gcc)
 * [gdb](#gdb)


<a name="git"/>

## Git

[Git](https://git-scm.com/) es una herramienta de versionado y manejo de
cambios en código fuente. Esta herramienta nos va a permitir compartir cambios
en código de una forma fácil y determinista.


### clone

```bash
$ git clone https://github.com/orgacomp/practicas practicas
```

El comando *clone* nos permite bajar a un directorio local un repositorio
remoto. En este caso el repositorio es el de las prácticas de la materia.


### status

```bash
practicas (main)$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

Status nos permite ver el estado actual de la copia de trabajo. En este caso no
hay ningún cambio. En el caso de haber nos indicará si son cambios a archivos
que son parte del repositorio o si son archivos nuevos.


### branch

Los branches son las líneas (o ramas) de desarrollo dentro de un repositorio.
Con el comando *branch* podemos ver las líneas locales.

```bash
practicas (main)$ git branch
practicas (main)$ git branch -a
```

La opción *-a* nos permite además ver los branches del repositorio remoto.


### checkout

Con el comando *checkout* podemos movernos entre _branches_ existentes o crear
nuevos.

```bash
practicas (main)$ git checkout branch_name
practicas (main)$ git checkout -b new_branch
```

### add

Si tenemos archivos nuevos que todavía no son parte del repositorio podemos
agregarlos con *add*.

```bash
practicas (main)$ git add new_file
```

El mismo comando se puede usar para agregar cambios de un archivo que ya es
parte del repositorio, pero es una buena práctica agregar los cambios de a poco
y conscientemente. Para eso se puede usar el comando *add -p*

```bash
practicas (main)$ git add -p
```

Este comando nos permite agregar interactivamente los cambios.


### commit

Una vez agregados los cambios con *add* utilizamos el comando *commit* para
decirle a git que los guarde en el repositorio.

```bash
practicas (main)$ git commit -m "Mensaje del commit"
practicas (main)$ git commit -v
```

### push

Con los cambios _commiteados_ podemos enviarlos al repositorio remoto con el
comando *push*.

```bash
practicas (main)$ git push
practicas (main)$ git push remote_name branch_name
```

### pull, fetch

Con el comando *pull* podemos traernos los cambios en el repositorio remoto y
aplicarlos en el _branch_ actual.

```bash
practicas (main)$ git pull
```

Si sólo queremos traer los cambios sin aplicarlos podemos usar el comando
*fetch*.

```bash
practicas (main)$ git fetch
```



<a name="docker"/>

## Docker

[Docker](https://www.docker.com/) nos va a permitir trabajar en un entorno
seguro y ya preparado con las herramientas necesarias.


### build

A partir de los Dockerfiles distribuidos con las prácticas podemos generar una
imagen para usar.

```bash
$ docker build . -t orga
```

Parados en el directorio donde esta el Dockerfile le pedimos a docker que
_buildee_ esa imagen y con *-t* le damos el nombre que queremos que use.


### images

Con *images* podemos ver la lista de imágenes que tenemos en este momento en el
sistema.

```bash
$ docker images
```

### run

Para correr la imagen y generar un container utilizamos el comando *run*.

```bash
$ docker run -it --rm orga
```

Con *-i* le decimos que sea interactivo, *-t* para que use una terminal tty y
*--rm* para que borre el container al terminar de usarlo. Para que esto sea
útil falta montar un directorio del host en el container.

```bash
$ docker run -v `pwd`:/home -it --rm orga
```

Esto le diría a docker que monte el directorio actual donde estamos ejecutando
docker en el directorio */home* del container.



<a name="qemu"/>

## QEMU

[QEMU](https://qemu.org/) es un emulador y virtualizador
[libre](https://en.wikipedia.org/wiki/Free_software). Esta herramienta nos va a
permitir ejecutar código compilado para diferentes arquitecturas sobre una
arquitectura base (x86_64).


Por ejemplo para ejecutar un binario *my_app_sparc* compilado para una
arquitectura sparc de 64bits usaríamos:

```bash
$ qemu-sparc64-static my_app_sparc
```



<a name="GCC"/>

## GCC

[GCC](https://www.gnu.org/software/gcc/) es el GNU C compiler. Esta herramienta
nos permite convertir un programa en lenguaje C a un programa en lenguaje
máquina. El proceso de conversión implica varios pasos:

* Pre compilación: toma el código C y reemplaza cualquier `#include`,
  `#define` y otras directivas que hayamos usado. Salida `prog.i`
* Compilación: toma el `prog.i` y convierte las instrucciones en código C a
  instrucciones en código ASM. Salida `prog.s`
* Assembly: toma el `prog.s` y reemplaza cada instrucción ASM por el código
  máquina correspondiente. Salida `prog.o`
* Linker: en el caso que tengamos más de un `.o` se encarga de unirlos y
  generar el binario final.

GCC realiza la compilación invocando a otros programas, en función de la tarea
a realizar. En nuestro caso, invoca a:

* `cpp` para preprocesar el código C
* `cc` para compilar el código C preprocesado.
* `as` para ensamblar el código assembly generado por `cc` (o manualmente).
* `ld` para enlazar binarios.

### Opciones de GCC

* `$ gcc -Og main.c`: compila el código utilizando el nivel de optimización
  `g`. Existen varios niveles de optimización:

   * `g` para que el asm sea lo más parecido al código c,
   * `s` para que optimice espacio,
   * `1`, `2` y `3` son optimizaciones de ejecución,
   * `fast` para que optimice en velocidad.

* `$ gcc -E main.c`: para detener la compilación luego de la etapa del
  Precompilador.
* `$ gcc -S main.c`: para detener la compilación luego de la etapa del
  Compilador.
* `$ gcc -c main.c`: para detener la compilación luego de la etapa del
  Assembly.
* `$ gcc -g main.c`: agrega símbolos de debugging al binario final.



<a name="GDB"/>

## GDB

[GDB](https://www.gnu.org/software/gdb/) es el GNU project debugger. Esta
herramienta nos permite ejecutar un programa paso a paso. No solo eso, sino que
podemos introducir cambios en la ejecución, como modificar variables o ejecutar
funciones, pararla en cualquier momento o ver el estado de la memoria.

La forma de ejecutarlo para debuggear un programa *my_app*:

```bash
$ gdb my_app 
```

Para que este comando sea útil debemos previamente haber compilado el programa
con opciones de debug (`gcc -g`). Una vez ejecutado *gdb* tendremos acceso a la
consola del programa donde podemos interactuar con el debbuger.

### Comandos de GDB

* `> run [args]`: inicia la ejecución del programa en background con los
  argumentos `[args]`.
* `> stop`: detiente la ejecución del programa en background.
* `> break bp`: le indica a gdb que al pasar por cierto lugar (`bp`) queremos
  que pare la ejecución. Por ejemplo `> b main` haría que al entrar en la
  función *main* pare la ejecución y nos permita inspeccionar el estado.
* `> next`: una vez parada la ejecución podemos ir ejecutando línea a línea.
* `> step`: next no entra en el código de la funciones. Usamos step.
* `> list`: imprime 10 lineas al rededor de la linea en la que se paró el
  programa.
* `> print var_name`: imprime la variable *var_name*. Por default la imprime en
  decimal pero con parámetros podemos indicarle que imprima de otra forma. Por
  ejemplo `> print /x x` imprime la variable x en formato hexadecimal.
* `> set var_name value`: escribe en la variable var\_name el valor value.
* `> shell sh_cmd`: podemos ejecutar comandos del shell directamente.
* `> make`:  es un comando de shell que tiene un trato especial y puede
  invocarse directamente.
* `> pipe gdb_cmd | sh_cmd`: podemos concatenar la salida de un comando gdb a
  un comando de shell. Por ejemplo `> pipe p x | grep red` hace un grep sobre
  la salida del print de la variable x. Esto puede abreviarse con el `|` en `>
  | p x | grep red` o incluso, si queremos repetir el último comando y pasarlo
  por un grep `> | | grep red`.
* `> layout`: gdb puede mostrar distintas ventanas en su interfaz ncurses. Con
  `> layout next` podemos ciclar por los predefinidos o crear nuevos.
* `> info registers`: imprime todos los registros del cpu.
