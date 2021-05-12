02 - Lenguaje de máquina
============================

## Introducción
### Manejo de punteros y tipos en C

Esta primera sección tiene como objetivo reafirmar algunas ideas relacionadas al manejo de punteros y tipos en C que serán útiles para comprender código máquina.
En esta sección se supone siempre una arquitectura de 64 bits.


1. Dadas las definiciones indicar el valor de las expresiones.

    ```c
    long a[] = {1, 100, 1000, 10000};
    ```
    1. sizeof(a):
    1. sizeof(\*a):
    1. sizeof(&a[0]):
    1. &a[3] - &a[1]:
    \
    &nbsp;
    ```c
    short b[] = {1, 100, 1000, 10000};
    ```
    1. sizeof(b):
    1. sizeof(\*b):
    1. sizeof(&b[0]):
    1. &b[3] - &b[1]:
    \
    &nbsp;
    ```c
    char *c = "abcdef";
    ```
    1. sizeof( c):
    1. \*(c+4):
    1. strlen(c+1):
    \
    &nbsp;
    ```c
    char *d = c;
    ```
    1. sizeof(d):
    1. sizeof(*d):
    1. \*(d+4):
    \
    &nbsp;
    ```c
    char e[] = "abcdee";
    ```
    1. sizeof(e):
    1. \*(e+1):
    1. e[1]:
    1. &e[4] - &e[0]:
    1. strlen(&e[2]):
    1. e[5] - e[4]:
    \
    &nbsp;
    ```c
    char f[] = {'a', 'b', 'c', 'd', 'e', 'e', '\0'};
    ```
    1. sizeof(f):
    1. \*(f+2):
    1. f[2]:
    1. strlen(&f[2]):


1. Dadas las definiciones indicar *sizeof* u *offset* según corresponda.

    ```c
    typedef struct {
        long l;
        char c;
        int;
    } a;

    typedef struct {
        int i;
        long l;
        char c;
        int j;
    } b;

    typedef struct {
        short v[9];
        int *x;
        char c;
    } c;
    
    typedef union {
        char *m;
        struct {
            int n;
            char x;
        } s;
    } d;
    ```

    sizeof(a):  
    offsetof(a, l):  
    offsetof(a, l):  
    offsetof(a, l):  
    
    sizeof(b):  
    offsetof(b, i):  
    offsetof(b, l):  
    offsetof(b, c):  
    offsetof(b, j):  
    
    sizeof( c):  
    offsetof(c, v):  
    offsetof(c, x):  
    offsetof(c, c):  
    
    sizeof(d):  
    offsetof(d, m):  
    offsetof(d, s):  

    > Hint: investigar la librería *stddef.h*.


## Código assembly

En los siguientes ejercicios supondremos siempre una arquitectura de 64 bits con código máquina x86-64 con sintaxis AT&T (a menos que se indique lo contrario).

1. Completar con un sufijo apropiado cada una de las siguientes instrucciones de código assembly.

    1. mov___ %rax, (%rdi)
    1. mov___ $0xf4, %bl
    1. mov___ (%rdx), %rax
    1. mov___ %eax, (%rsp)
    1. mov___ %cx, (%rax)
    1. mov___ (%rax), %si
    1. mov___ %r8, (%rsi)
    1. mov___ (%rsp, %rdi, 4), %sil

1. Asumiendo que las variables o y d son de los tipos *origen_t* y *dest_t* declarados con *typedef*, se busca implementar el siguiente movimiento:

    ```c
    origen_t *o;
    dest_t *d;
  
    *dp = (dest_t) *sp; 
    ```
    
    Escribir las instrucciones de código assembly apropiadas para realizar los movimientos de datos indicados con formato origen_t -> dest_t.
    La primera instrucción debe leer memoria, realizar la conversión apropiada y setear la porción apropiada de %rax y la segunda debe escribir la porción de %rax seteada en memoria.
  
    Ejemplo: long -> long:  
  
    ```
    movq (%rdi), %rax
    movq %rax, (%rsi)
    ```
  
    1. short -> short
    1. short -> long
    1. char -> int  
    1. char -> unsigned
    1. int -> char
    1. char -> short

1. Proveer la implementación en código assembly de las siguientes funciones escritas en C. Considerar el siguiente ejemplo:

    Bloque de código C:
    ```c
    long long_to_long(long x) {
    return x;
    }
    ```
    Implementación en código assembly:
    ```
    long_to_long:
        movq    %rdi, %rax
        ret
    ```
    \
    &nbsp;
    1.
    ```c
    long int_to_long(int x) {
        return x;
    }
    ```
    
    2.
    ```c
    long short_to_long(short x) {
        return x;
    }
    ```
    
    3.
    ```c
    long schar_to_long(signed char x) {
        return x;
    }
    ```
    
    4.
    ```c
    long ushort_to_long(unsigned short x) {
        return x;
    }
    ```
    
    5.
    ```c
    long uchar_to_long(unsigned char x) {
        return x;
    }
    ```
    
    6.
    ```c
    long unsigned_to_long(unsigned x) {
        return x;
    }
    ```
