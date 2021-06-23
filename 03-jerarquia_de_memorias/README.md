# 03 - Jerarquía de memorias

## Localidad

Los siguientes ejercicios tienen como objetivo afianzar conceptos clave en el entendimiento de la jerarquía de memorias centrándose en la propiedad fundamental de los programas de computadora: la localidad.

Los programas con buena localidad tienden a acceder al mismo set de datos una y otra vez o a acceder a sets cercanos de datos. De este modo, tienden a acceder a más datos de los niveles más altos de la jerarquía de memorias que programas con mala o pobre localidad y, por lo tanto, corren más rápido.


1. Dada la siguiente función, indicar qué está computando y permutar los loops de modo que se itere sobre el arreglo tridimensional *array* con el patrón de acceso *stride-1*.

    ```c
    int foo(int array[N][N][N]) {
        int i, j, k, product = 1;
    
        for (i = N-1; i >= 0; i--) {
            for (j = N-1; j >= 0; j--) {
                for (k = N-1; k >= 0; k--) {
                    product *= array[j][k][i];
                }
            }
        }
        return product;
    }
    ```

1. Dadas las definiciones:

    ```c
    # define N 1000
    
    typedef struct {
        int vel[3];
        int acc[3];
    } point;
    
    point p[N];
    ```

    Analizar las siguientes 3 funciones, indicar qué operación realizan, ordenarlas según su localidad espacial y justificar con las consideraciones que llevaron a elegir ese orden.

    ```c
    void foo1(point *p, int n) {
        int i, j;
      
        for (i = 0; i < n; i++) {
            for (j = 0; j < 3; j++)
                p[i].vel[j] = 0;
            for (j = 0; j < 3; j++)
                p[i].acc[j] = 0;
        }
    }
    
    void foo2(point *p, int n) {
        int i, j;
      
        for (i = 0; i < n; i++) {
             for (j = 0; j < 3; j++) {
                p[i].vel[j] = 0;
                p[i].acc[j] = 0;
             }
        }
    }
    
    void foo3(point *p, int n) {
        int i, j;
    
        for (j = 0; j < 3; j++) {
            for (i = 0; i < n; i++)
                p[i].vel[j] = 0;
            for (i = 0; i < 3; i++)
                p[i].acc[j] = 0;
        }
    }
    ```


## Memoria Caché

Una caché es un dispositivo de almacenamiento más rápido y de menor capacidad que actúa como *staging area* de un subconjunto de datos almacenados en un dispositivo más lento y de mayor capacidad. En los siguientes ejercicios buscaremos comprender sus características y mecanismos.



1. Completar la siguiente tabla de parámetros de distintas cachés determinando cantidad de sets (S), cantidad de bits de tag (t), cantidad de bits para el set index (s) y cantidad de bits para el block offset (b).

    | Cache  |  m   |  C   |  B  |  E  |  S  |  t  |  s  |  b  |
    | ------ | ---- | ---- | --- | --- | --- | --- | --- | --- |
    |   1.   |  32  | 1024 |  4  |  1  |     |     |     |     |
    |   2.   |  32  | 1024 |  8  |  4  |     |     |     |     |
    |   3.   |  32  | 1024 | 32  | 32  |     |     |     |     |

1. Dada una caché de 2048 bytes con mapeo directo y bloques de 32 bytes, las definiciones a continuación y suponiendo que:

    - El *sizeof* corresponde a una arquitectura x86 (32 bits).
    - La variable cuadrado comienza en la dirección 0.
    - La memoria caché está inicialmente vacía.
    - Los únicos accesos a memoria son al arreglo, las variables i y j se almacenan en registros.
    
    ```c
    struct color {
        int c;
        int m;
        int y;
        int k;
    };
    
    struct color cuadrado[16][16];
    
    int i, j;
    ```

    Indicar qué porcentaje de escrituras en la caché fallará para cada uno de los siguientes fragmentos de código C:

    Fragmento a:
    ```c
    for (i=0; i < 16; i++) {
        for (j=0; j < 16; j++) {
            cuadrado[i][j].c = 0;
            cuadrado[i][j].m = 0;
            cuadrado[i][j].y = 1;
            cuadrado[i][j].k = 0;
        }
    }
    ```
    
    Fragmento b:
    ```c
    for (i=0; i < 16; i++) {
        for (j=0; j < 16; j++) {
            cuadrado[j][i].c = 0;
            cuadrado[j][i].m = 0;
            cuadrado[j][i].y = 1;
            cuadrado[j][i].k = 0;
        }
    }
    ```
    
    Fragmento c:
    ```c
    for (i=0; i < 16; i++) {
        for (j=0; j < 16; j++) {
            cuadrado[j][i].y = 1;
        }
    }
    for (i=0; i < 16; i++) {
        for (j=0; j < 16; j++) {
            cuadrado[j][i].c = 0;
            cuadrado[j][i].m = 0;
            cuadrado[j][i].k = 0;
        }
    }
    ```

1. En una caché que usa los `s` bits de orden más alto de una dirección como _set index_, bloques contiguos de memoria son mapeados al mismo set. Considerando este tipo de caché responder:

    1. ¿Cuántos bloques hay en cada uno de estos pedazos contiguos de array?
    1. Dada una caché con: (S, E, B, m) = (512, 1, 32, 32) y considerando el siguiente código, responder cuál será la máxima cantidad de bloques del array que se almacenarán en la caché en algún momento de la ejecución?
    
    ```c
    int array[4096];
    for (i = 0; i < 4096; i++)
        sum += array[i];
    ```

