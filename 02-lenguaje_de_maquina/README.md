# 02 - Lenguaje de máquina

## Introducción

### Manejo de punteros y tipos en C

Esta primera sección tiene como objetivo reafirmar algunas ideas relacionadas
al manejo de punteros y tipos en C que serán útiles para comprender código
máquina.
En esta sección se supone siempre una arquitectura de 64 bits.


1. Dadas las definiciones indicar el valor de las expresiones.

    ```c
    long a[] = {1, 100, 1000, 10000};
    ```
    1. sizeof(a):
    1. sizeof(\*a):
    1. sizeof(&a[0]):
    1. &a[3] - &a[1]:

    ```c
    short b[] = {1, 100, 1000, 10000};
    ```
    1. sizeof(b):
    1. sizeof(\*b):
    1. sizeof(&b[0]):
    1. &b[3] - &b[1]:

    ```c
    char *c = "abcdef";
    ```
    1. sizeof( c):
    1. \*(c+4):
    1. strlen(c+1):

    ```c
    char *d = c;
    ```
    1. sizeof(d):
    1. sizeof(*d):
    1. \*(d+4):

    ```c
    char e[] = "abcdee";
    ```
    1. sizeof(e):
    1. \*(e+1):
    1. e[1]:
    1. &e[4] - &e[0]:
    1. strlen(&e[2]):
    1. e[5] - e[4]:

    ```c
    char f[] = {'a', 'b', 'c', 'd', 'e', 'e', '\0'};
    ```
    1. sizeof(f):
    1. \*(f+2):
    1. f[2]:
    1. strlen(&f[2]):


1. Dadas las definiciones indicar *sizeof* u *offset* según corresponda.

   a.

      ```c
      typedef struct {      typedef struct {
          long l;               long l;
          char c;               char c;
          int i;                int i;
      } a;                  } __attribute__ ((packed)) a_packed;
      ```

      1. sizeof(a):
      1. offsetof(a, l):
      1. offsetof(a, i):
      1. offsetof(a, c):

   b.

      ```c
      typedef struct {      typedef struct {
          int i;                int i;
          long l;               long l;
          char c;               char c;
          int j;                int j;
      } b;                  } __attribute__ ((packed)) b_packed;
      ```

      1. sizeof(b):
      1. offsetof(b, i):
      1. offsetof(b, l):
      1. offsetof(b, c):
      1. offsetof(b, j):

   c.

      ```c
      typedef struct {      typedef struct {
          short v[9];           short v[9];
          int *x;               int *x;
          char c;               char c;
      } c;                  } __attribute__ ((packed)) c_packed;
      ```

      1. sizeof( c):
      1. offsetof(c, v):
      1. offsetof(c, x):
      1. offsetof(c, c):

   d.

      ```c
    typedef union {
        char *m;
        struct {
            int n;
            char x;
        } s;
    } d;
    ```

      1. sizeof(d):
      1. offsetof(d, m):
      1. offsetof(d, s):

    > Hint: investigar la librería *stddef.h*.


1. Probar los programas que se generan con el siguiente código C en
   arquitecturas x86-64 y SPARC y analizar el resultado.

   ```c
   #include <stdio.h>
   #include <stddef.h>

   typedef struct {
       unsigned char role;
       int hp;
   } __attribute__((packed)) character;

   int main(void) {
       character ex[2] = {{0x35, 100}, {0xaf, 127}};
       int *php_0 = &ex[0].hp;
       int *php_1 = &ex[1].hp;

       printf("sizeof(character) = %lu\n", sizeof(character));
       printf("offsetof(character, role) = %lu\n", offsetof(character, role));
       printf("offsetof(character, hp) = %lu\n", offsetof(character, hp));

       printf("ex[0].hp = %d\n", ex[0].hp);
       printf("ex[1].hp = %d\n", ex[1].hp);

       printf("php_0 = %p\n", (void*)php_0);
       printf("php_1 = %p\n", (void*)php_1);

       printf("*php_0 = %d\n", *php_0);
       printf("*php_1 = %d\n", *php_1);

       return 0;
   }
   ```

### Proceso de compilación

1. Hacer un programa en C, sin includes, que sume dos variable. El main debe
   devolver `1` si la suma da mayor que una constante `#define VAR_MAX 100`, `0`
   en caso contrario. Conseguir el pre compilado, el código assembler y el código
   maquina del programa.

    > Hint: usar las diferentes opciones de gcc, xdd, y objdump.


## Código assembly

En los siguientes ejercicios supondremos siempre una arquitectura de 64 bits
con código máquina x86-64 con sintaxis AT&T (a menos que se indique lo
contrario).

1. Dada la siguiente carga de valores en memoria y registros respectivamente

    | Dirección | Valor |
    | --------- | ----- |
    | 0x100     | 0xFF  |
    | 0x104     | 0xAB  |
    | 0x108     | 0x13  |
    | 0x10C     | 0x11  |
    | --------- | ----- |

    | Registro | Valor |
    | -------- | ----- |
    | `%rax`   | 0x100 |
    | `%rcx`   | 0x1   |
    | `%rdx`   | 0x3   |
    | -------- | ----- |

    Completar con el tipo de operando y el valor equivalente de los siguientes
    operandos:

    | Operando          | Tipo | Valor |
    | ----------------- | ---- | ----- |
    | `%rax`            |      |       |
    | `0x104`           |      |       |
    | `$0x108`          |      |       |
    | `(%rax)`          |      |       |
    | `4(%rax)`         |      |       |
    | `9(%rax, %rdx)`   |      |       |
    | `260(%rcx, %rdx)` |      |       |
    | `0xFC(, %rcx, 4)` |      |       |
    | `(%rax, %rdx, 4)` |      |       |

1. Completar con un sufijo apropiado cada una de las siguientes instrucciones
   de código assembly.

    1. `mov___ %rax, (%rdi)`
    1. `mov___ $0xf4, %bl`
    1. `mov___ (%rdx), %rax`
    1. `mov___ %eax, (%rsp)`
    1. `mov___ %cx, (%rax)`
    1. `mov___ (%rax), %si`
    1. `mov___ %r8, (%rsi)`
    1. `mov___ (%rsp, %rdi, 4), %sil`

1. Indicar en cada caso por que no es una instrucción válida.

    1. `movb 0xF, (%ebx)`
    1. `movl %rax, (%rsp) `
    1. `movw (%rax), 4(%rsp)`
    1. `movb %al, %sl`
    1. `movq %rax, $0x123`
    1. `movl %eax, %rdx`
    1. `movb %si, 8(%rbp)`

1. Asumiendo que las variables o y d son de los tipos *origen_t* y *dest_t*
   declarados con *typedef*, se busca implementar el siguiente movimiento:

    ```c
    origen_t *o;
    dest_t *d;

    *dp = (dest_t) *sp;
    ```

    Escribir las instrucciones de código assembly apropiadas para realizar los
    movimientos de datos indicados con formato origen_t -> dest_t.

    La primera instrucción debe leer memoria, realizar la conversión apropiada
    y setear la porción apropiada de %rax y la segunda debe escribir la porción
    de %rax seteada en memoria.

    Ejemplo: long -> long:

    ```
    movq (%rdi), %rax
    movq %rax, (%rsi)
    ```

    1. `short` -> `short`
    1. `short` -> `long`
    1. `char` -> `int`
    1. `char` -> `unsigned`
    1. `int` -> `char`
    1. `char` -> `short`

1. Indicar el valor de `%rax` para cada linea del siguiente código asm.
    ```
    example:
        movabsq $0x0011223344556677, %rax
        movb $0xaa, %dl
        movb %dl, %al
        movsbq %dl, %rax
        movzbq %dl, %rax
    ```

1. Proveer la implementación en código assembly de las siguientes funciones
   escritas en C. Considerar el siguiente ejemplo:

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

1. Dado el siguiente código asm escribir una función en C que se compile a lo
   mismo.

   > Hint: utilizar GCC para corroborar el resultado.

   ```
   decode1:
       movq (%rdi), %r8
       movq (%rsi), %rcx
       movq (%rdx), %rax
       movq %r8, (%rsi)
       movq %rcx, (%rdx)
       movq %rax, (%rdi)
       ret
    ```

   El prototipo de la función debe ser:
   ```C
   void decode1(long *xp, long *yp, long *zp)
   ```
   Se debe suponer ademas que el primer operando se guarda en `%rdi`, el
   segundo en `%rsi` y el ultimo en `%rdx`.

1. Indicar con que instrucción asm se pueden reemplazar los siguiente códigos
   en asm.

   1.
   ```
   subq $8, %rsp
   movq %rbp, (%rsp)
   ```

   1.
   ```
   movq (%rsp), %rax
   addq $8, %rsp
   ```
