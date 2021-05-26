# 02 - Lenguaje de máquina

## Introducción

### Manejo de punteros y tipos en C

Esta primera sección tiene como objetivo reafirmar algunas ideas relacionadas
al manejo de punteros y tipos en C que serán útiles para comprender código
máquina.
En esta sección se supone siempre una arquitectura de 64 bits.


1. Dadas las definiciones indicar el valor de las expresiones.

    1. Dado:
        ```c
        long a[] = {1, 100, 1000, 10000};
        ```
        Indicar:
        1. `sizeof(a)`
        1. `sizeof(*a)`
        1. `sizeof(&a[0])`
        1. `&a[3] - &a[1]`

    1. Dado:
        ```c
        short b[] = {1, 100, 1000, 10000};
        ```
        Indicar:
        1. `sizeof(b)`
        1. `sizeof(*b)`
        1. `sizeof(&b[0])`
        1. `&b[3] - &b[1]`

    1. Dado:
        ```c
        char *c = "abcdef";
        ```
        Indicar:
        1. `sizeof(c)`
        1. `*(c+4)`
        1. `strlen(c+1)`

    1. Dado:
        ```c
        char *d = c;
        ```
        Indicar:
        1. `sizeof(d)`
        1. `sizeof(*d)`
        1. `*(d+4)`

    1. Dado:
        ```c
        char e[] = "abcdee";
        ```
        Indicar:
        1. `sizeof(e)`
        1. `*(e+1)`
        1. `e[1]`
        1. `&e[4] - &e[0]`
        1. `strlen(&e[2])`
        1. `e[5] - e[4]`

    1. Dado:
        ```c
        char f[] = {'a', 'b', 'c', 'd', 'e', 'e', '\0'};
        ```
        Indicar:
        1. `sizeof(f)`
        1. `*(f+2)`
        1. `f[2]`
        1. `strlen(&f[2])`

1. Dadas las definiciones indicar *sizeof* u *offset* según corresponda.
    1. Dado:
        ```c
        typedef struct {
            long l;
            char c;
            int i;
        } __attribute__ ((packed)) a_packed;
        typedef struct {
            long l;
            char c;
            int i;
        } a;
        ```
        Indicar:
        1. `sizeof(a)`
        1. `offsetof(a, l)`
        1. `offsetof(a, i)`
        1. `offsetof(a, c)`

    1. Dado:
        ```c
        typedef struct {
            int i;
            long l;
            char c;
            int j;
        } __attribute__ ((packed)) b_packed;
        typedef struct {
            int i;
            long l;
            char c;
            int j;
        } b;
        ```
        Indicar:
        1. `sizeof(b)`
        1. `offsetof(b, i)`
        1. `offsetof(b, l)`
        1. `offsetof(b, c)`
        1. `offsetof(b, j)`

    1. Dado:
        ```c
        typedef struct {
            short v[9];
            int *x;
            char c;
        } __attribute__ ((packed)) c_packed;
        typedef struct {
            short v[9];
            int *x;
            char c;
        } c;
        ```
        Indicar:
        1. `sizeof( c)`
        1. `offsetof(c, v)`
        1. `offsetof(c, x)`
        1. `offsetof(c, c)`

    1. Dado:
        ```c
        typedef union {
            char *m;
            struct {
                int n;
                char x;
            } s;
        } d;
        ```
        Indicar:
        1. `sizeof(d)`
        1. `offsetof(d, m)`
        1. `offsetof(d, s)`

    > Hint: investigar la librería *stddef.h*.


1. Probar el programa que se genera con el siguiente código C (y si se tiene
   acceso a una arquitectura SPARC o ARM, probarlo también en dichas
   arquitecturas) y analizar su resultado.

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

   #if defined(__GNUC__)
   # if defined(__i386__)
           /* Enable Alignment Checking on x86 */
           __asm__("pushf\norl $0x40000,(%esp)\npopf");
   # elif defined(__x86_64__)
            /* Enable Alignment Checking on x86_64 */
           __asm__("pushf\norl $0x40000,(%rsp)\npopf");
   # endif
   #endif

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

    | Registro | Valor |
    | -------- | ----- |
    | `%rax`   | 0x100 |
    | `%rcx`   | 0x1   |
    | `%rdx`   | 0x3   |

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

1. Dadas que las variables op y dp, de los tipos *origen_t* y *dest_t*,
   respectivamente, declarados con *typedef*, se busca implementar el siguiente
   movimiento:

    ```c
    origen_t *op;
    dest_t *dp;

    *dp = (dest_t) *op;
    ```

    Escribir las instrucciones de código assembly apropiadas para realizar los
    movimientos de datos indicados con formato origen_t -> dest_t.

    Suponer que los valores de op y dp están almacenados en %rdi y %rsi
    respectivamente.

    La primera instrucción debe leer memoria, realizar la conversión correcta
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
    ```nasm
    example:
        movabsq $0x0011223344556677, %rax
        movb $0xaa, %dl
        movb %dl, %al
        movsbq %dl, %rax
        movzbq %dl, %rax
    ```

1. Dado el siguiente código asm escribir una función en C que se compile a lo
   mismo.

   > Hint: utilizar GCC para corroborar el resultado.

   ```nasm
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
   ```nasm
   subq $8, %rsp
   movq %rbp, (%rsp)
   ```

   1.
   ```nasm
   movq (%rsp), %rax
   addq $8, %rsp
   ```

1. Escribir un programa en assembler utilizando únicamente `leaq` que
   implementa la siguiente función en C:

   ```C
   long poly(long x, long y, long z)
   {
       long p = 2 * x + 6 * y + 6 * z;
       return p;
   }
   ```

1. Dada la siguiente carga de valores en memoria y registros respectivamente

    | Dirección | Valor |
    | --------- | ----- |
    | 0x100     | 0xFF  |
    | 0x104     | 0xAB  |
    | 0x110     | 0x13  |
    | 0x118     | 0x11  |

    | Registro | Valor |
    | -------- | ----- |
    | `%rax`   | 0x100 |
    | `%rcx`   | 0x1   |
    | `%rdx`   | 0x3   |

   Indicar para cada linea del siguiente código asm el destino de la operación
   (donde se guarda el resultado) y cual es el resultado de la operación.

    | Código                       | Destino | Valor |
    | ---------------------------- | ------- | ----- |
    | `addq %rcx, (%rax)`          |         |       |
    | `subq %rdx, 4(%rax)`         |         |       |
    | `imulq $16, (%rax, %rdx, 8)` |         |       |
    | `incq 16(%rax)`              |         |       |
    | `decq %rcx`                  |         |       |
    | `subq %rdx, %rax`            |         |       |

1. Para la siguiente instrucción:

    ```nasm
    xorq %rcx, %rcx
    ```

    Indicar:
    1. Que función realiza?
    1. Con que otra operación puede ser reemplazada?
    1. Por que es preferible utilizar la primera y no la segunda?


1. Dado el siguiente código en C, escribir el código ASM al que compila.

   ```C
   #include <inttypes.h>

   typedef unsigned __int128 uint128_t;

   void producto_unsigned(uint128_t *dest, uint64_t x, uint64_t y) {
       *dest = x * (uint128_t) y;
   }
   ```

   Los parámetros son dados en `%rdi`, `%rsi` y `%rdx` respectivamente.

1. Dado el siguiente código en C, escribir el código ASM al que compila.
   Indicar como cambia el código ASM si los parámetros de la función pasan a
   ser unsigned.

   ```C
   void div_signed(long x, long y, long *qp, long *rp)
   {
       long q = x / y;
       long r = x % y;
       *qp = q;
       *rp = r;
   }
   ```

   Los parámetros son dados en `%rdi`, `%rsi`, `%rdx` y `%rcx` respectivamente.

1. Para la siguiente función en C:

   ```C
   int comp(data_t a, data_t b){
       return a COMP b;
   }
   ```

   Donde COMP se define mediante `#define`. Y suponiendo que `a` se guarda en
   `%rdi`, y `b` en `%rsi`. Completar la siguiente tabla:

   | ASM | COMP | data_t |
   | --- | ---- | ------ |
   | `cmpl %esi, %edi`<br>`setl %al`| | |
   | `cmpw %si, %di`<br>`setge %al`| | |
   | `cmpb %sil, %dil`<br>`setbe %al`| | |
   | `cmpq %rsi, %rdi`<br>`setne %al`| | |

1. Para la siguiente función en C:

   ```C
   int test(data_t a, data_t b){
       return a TEST b;
   }
   ```

   Donde TEST se define mediante `#define`. Y suponiendo que `a` se guarda en
   `%rdi`. Completar la siguiente tabla:

   | ASM | TEST | data_t |
   | --- | ---- | ------ |
   | `testq %rdi, %rdi`<br>`setge %al`| | |
   | `testw %di, %di`<br>`sete %al`| | |
   | `testb %dil, %dil`<br>`seta %al`| | |
   | `testl %edi, %edi`<br>`setle %al`| | |

1. Indicar cual es el target de `je` indicado con `xxxxxx`.
   1. Dado:
        ```nasm
        40003FA: 74 02     je xxxxxx
        40003FC: FF D0     callq *%rax
        ```
   1. Dado:
        ```nasm
        400042F: 74 F4     je xxxxxx
        4000431: 5D        pop %rbp
        ```
   1. Dado:
        ```nasm
        xxxxxxx: 77 02     ja 400547
        xxxxxxx: 5D        pop %rax
        ```
   1. Dado:
        ```nasm
        40005E8: E9 73 FF FF FF    jmpq xxxxxx
        40005EF: 90                nop
        ```

1. Dado el siguiente código en C que compila al código asm que lo continúa.

   ```C
   void cond(short a, short *p)
   {
       if (a && *p > a)
           *p = a;
   }
   ```

   ```nasm
   cond:
       testq %rdi, %rdi
       je .L1
       cmpq %rsi, (%rdi)
       jle .L1
       movq %rdi, (%rsi)
    .L1:
       ret
   ```
   1. Por que en el código asm hay dos branches condicionales si en el código C
      solo hay uno?
   1. Escribir un código en C utilizando `goto` que tenga una mayor correlación
      con el código asm.

1. A partir de la versión completa del siguiente código C, se obtuvo el código
   assembly que le sigue. Analizando el código assembly, completar el código C
   de forma tal que al compilar se obtenga el mismo código assembly.

   ```C
   short test(short x, short y, short z)
   {
       short val = ____________;
       if (____________)
       {
           if (____________)
           {
               val = ____________;
           } else {
               val = ____________;
           }
       } else if (____________) {
           val = ____________;
       }
       return val;
   }
   ```

   ```nasm
   test:
       leaq (%rdx,%rsi), %rax
       subq %rdi, %rax
       cmpq $5, %rdx
       jle .L2
       cmpq $2, %rsi
       jle .L3
       movq %rdi, %rax
       idivq %rdx, %rax
       ret
   .L3:
       movq %rdi, %rax
       idivq %rsi, %rax
       ret
   .L2:
       cmpq $3, %rdx
       jge .L4
       movq %rdx, %rax
       idivq %rsi, %rax
   .L4:
       rep; ret
   ```

1. A partir de la versión completa del siguiente código C, se obtuvo el código
   assembly que le sigue. Analizando el código assembly, completar el código C
   de forma tal que al compilar se obtenga el mismo código assembly.

   ```C
   short test(short x, short y, short z)
   {
       short val = ____________;
       if (____________)
       {
           if (____________)
           {
               val = ____________;
           } else {
               val = ____________;
           }
       } else if (____________) {
           val = ____________;
       }
       return val;
   }
   ```

   ```nasm
   test:
       leaq 12(%rsi), %rdx
       testq %rdi, %rdi
       jge .L2
       movq %rdi, %rbx
       imulq %rsi, %rbx
       movq %rdi, %rdx
       orq %rsi, %rdx
       cmpq %rsi, %rdi
       cmovge %rdx, %rbx
       ret
   .L2:
       idivq %rsi, %rdi
       cmpq $10, %rsi
       cmovge %rdi, %rbx
       ret
   ```

1. A partir de la versión completa del siguiente código C, se obtuvo el código
   assembly que le sigue. Analizando el código assembly, completar el código C
   de forma tal que al compilar se obtenga el mismo código assembly.

   ```C
   short loop_while(short a, short b)
   {
       short result = ____________;
       while (____________)
       {
           result = ____________;
           a = ____________;
       }
       return result;
   }
   ```

   ```nasm
   loop_while:
       movl $0, %eax
       jmp .L2
   .L3:
       leaq (,%rsi, %rdi), %rdx
       addq %rdx, %rax
       subq $1, %rdi
   .L2:
       cmpq %rsi, %rdi
       jg .L3
       ret
   ```

1. Implementar las funciones `strchr()` y `strrchr()` en lenguaje ensamblador.
   Una de ellas en x86 (32 bits), la otra en x86-64 (64 bits).

   Escribir una porción de código en lenguaje ensamblador donde se invoque,
   correctamente, a cada función implementada.

    ```
    char *strchr(const char *s, int c);
    char *strrchr(const char *s, int c);

    La función strchr() retorna un puntero a la primera ocurrencia del
        caracter c en la cadena s.
    La función strrchr() retorna un puntero a la última ocurrencia del
        caracter c en la cadena s.

    Las funciones strchr() y strrchr() retornan un puntero al caracter o
    NULL si el caracter no se encuentra. El byte nulo que termina la cadena
    es considerado parte de la misma, si c es especificado como '\0', estas
    funciones retornan un puntero al terminador.
    ```

1. Recuperar la definición de una estructura desconocida sabiendo que la misma
   es pasada como argumento (como puntero) en cada una de las siguientes
   funciones assembly.

    ```nasm
    _f1:
            movl    4(%rdi), %eax
            ret
    _f2:
            leaq    8(%rdi), %rax
            ret
    _f3:
            movsbq  40(%rdi), %rax
            cmpq    %rax, 32(%rdi)
            setb    %al
            ret
    _f4:
            movl    $0, %edx
            movl    $0, %eax
            jmp .L5
    .L6:
            movswl  8(%rdi,%rdx,2), %ecx
            addl    %ecx, %eax
            addq    $1, %rdx
    .L5:
            cmpq    $6, %rdx
            jbe .L6
            rep ret
    _f5:
            movsbw  (%rdi), %ax
            ret
    _f6:
            leaq    24(%rdi), %rax
            ret
    _f7:
            movl    $48, %eax
            ret
    _f8:
            movsd   24(%rdi), %xmm0
            addsd   %xmm0, %xmm0
            ret
    _f9:
            movzwl  42(%rdi,%rsi,2), %eax
            ret
    ```

1. El código assembly de la siguiente función posee bugs que llevan a un
   incorrecto funcionamiento ¿cuáles son, por qué y cómo se subsanan?.
    ```c
     1: typedef struct element {
     2:     char id[4];
     3:     union {
     4:         double d;
     5:         unsigned char b[8];
     6:     } ;
     7: } element_t;
     8:
     9: typedef struct nodo {
    10:     struct element * dato;
    11:     struct nodo * siguiente;
    12: } * lista_t;
    13:
    14: extern void funcion(struct element *);
    15:
    16: element_t * lista_buscar(lista_t lista, const char * id) {
    17:     for (struct nodo * nodo = lista; nodo; nodo = nodo->siguiente) {
    18:         if(!strcmp(lista->dato->id, id))
    19:             return lista->dato;
    20:     }
    21:     return NULL;
    22: }
    ```
    ```nasm
     1: lista_buscar:
     2:         pushq   %rbp
     3:         pushq   %rbx
     4:         addq    $8, %rsp
     5:         movq    %rdi, %r12
     6:         movq    %rsi, %r13
     7:         movq    %rdi, %rbx
     8: .L7:
     9:         testq   %rbx, %rbx
    10:         je      .L6
    11:         leaq    (%r12), %rbp
    12:         movq    %r13, %rsi
    13:         movq    %rbp, %rdi
    14:         call    strcmp
    15:         testq   %eax, %eax
    16:         je      .L10
    17:         movq    8(%rbx), %rbx
    18:         jmp     .L7
    19: .L10:
    20:         movq    %rbp, %rbx
    21: .L6:
    22:         movq    %rbx, %rax
    23:         subq    $8, %rsp
    24:         popq    %rbp
    25:         popq    %rbx
    26:         ret
    ```

1. Dado el siguiente código C, calcular el tamaño de la estructura `digimon_t`
   y del arreglo `party` tanto _packed_ como con requerimientos de
   alineamiento e implementar la función `attacks()`.

    ```c
     1: typedef uint64_t (*digiattack_t) (struct digimon *, struct digimon *);
     2:
     3: typedef struct digimon {
     4:     uint32_t id;
     5:     uint8_t type;
     6:     uint16_t attributes;
     7:     uint32_t family;
     8:     digiattack_t * attacks;
     9:     uint16_t hp;
    10:     uint32_t ep;
    11:     uint8_t lvl;
    12: } digimon_t;
    13:
    14: digimon_t party[4];
    15:
    16: uint64_t attacks(void) {
    17:     uint64_t total = 0;
    18:
    19:     for (size_t i = 0; i < sizeof party / sizeof *party; i++ ) {
    20:         total += party[i].attacks[i](enemy_party, party);
    21:     }
    22:
    23:     return total;
    24: }
    ```

1. A partir de la versión completa del siguiente código C, se obtuvo el código
   assembly que le sigue. Analizando el código assembly, completar el código C
   de forma tal que al compilar se obtenga el mismo código assembly. ¿Cuánto
   valen las constantes `FILAS` y `COLUMNAS`?.

    ```c
     1: int mglobal[FILAS][COLUMNAS];
     2:
     3: long int funcion(size_t f, size_t c, int * v) {
     4:     size_t i, j;
     5:     *v = ____________;
     6:     for (i = ____________; ____________; ____________) {
     7:         mglobal[i][i] = ____________;
     8:         for (j = ____________; ____________; ____________) {
     9:             mglobal[i][i] += ____________;
    10:         }
    11:         *v += ____________;
    12:     }
    13:     return (*v > sizeof(mglobal)) ? ____________ : -1;
    14: }
    ```

    ```nasm
     1: funcion:
     2:     movl    $0, %r8d
     3:     movl    $-7, (%rdx)
     4:     jmp .L2
     5: .L5:
     6:     leaq    (%r8,%r8,2), %rax
     7:     salq    $5, %rax
     8:     movl    $-1, mglobal(%rax)
     9:     leaq    1(%r8), %r11
    10:     movq    %r11, %r9
    11:     jmp .L3
    12: .L4:
    13:     leaq    (%r8,%r8), %rax
    14:     leaq    (%rax,%r8), %rcx
    15:     salq    $3, %rcx
    16:     subq    %r8, %rcx
    17:     addq    %r9, %rcx
    18:     addq    %r8, %rax
    19:     salq    $5, %rax
    20:     movl    mglobal(%rax), %r10d
    21:     addl    mglobal(,%rcx,4), %r10d
    22:     movl    %r10d, mglobal(%rax)
    23:     addq    $1, %r9
    24: .L3:
    25:     cmpq    %rsi, %r9
    26:     jb  .L4
    27:     leaq    (%r8,%r8,2), %rax
    28:     salq    $5, %rax
    29:     movl    mglobal(%rax), %eax
    30:     addl    %eax, (%rdx)
    31:     movq    %r11, %r8
    32: .L2:
    33:     cmpq    %rdi, %r8
    34:     jb  .L5
    35:     movl    (%rdx), %edx
    36:     movslq  %edx, %rax
    37:     cmpl    $1289, %edx
    38:     movq    $-1, %rdx
    39:     cmovb   %rdx, %rax
    40:     ret
    ```
