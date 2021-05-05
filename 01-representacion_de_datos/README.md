01 - Representación de datos
============================

El objetivo de esta práctica es ganar agilidad en la conversión y trabajo con
números *a ojo* y saber cómo utilizar código C para no perder la cabeza. La
conversión *a ojo* suele ser muy útil en el momento de leer código asembler ya
que en general los números estarán representados en hexadecimal o en binario.

1. Convertir los siguientes números en representación decimal a binario (16bits)
    1. 18265
    1. 7810
    1. 51007
    1. 66425
    1. 31530
    1. 19725
    1. 5736
    1. 423

1. Escribir un programa en C que, utilizando *printf* y *scanf*, resuelva el
   ejercicio anterior.

   > Hint: El siguiente código describe un programa que toma el número decimal
   > ingresado por el usuario y lo imprime en la misma representación.

   ```c 
   #include <stdio.h>
   
   int main(void)
   {
       unsigned int entered_number;
   
       printf("Enter a number in decimal: ");
       scanf("%u", &entered_number);
       printf("Decimal: %d\n", entered_number);
   
       return 0;
   }
   ``` 

1. Convertir los siguientes números en representación hexadecimal a binario (16bits)
    1. 0xdc2d
    1. 0x9b7a
    1. 0xfdd8
    1. 0xe882
    1. 0xe8b2
    1. 0x6e49
    1. 0x235e
    1. 0x3343
    1. 0x39d1
    1. 0xf093

1. Escribir un programa en C que utilizando *printf* y *scanf* resuelva el
   ejercicio anterior. El número debe ser ingresado en formato *0x1234*.

   > Hint: utilizar los distintos formatos aceptados por la función *printf* y *scanf*.

1. Convertir los siguientes números en representación binaria a hexadecimal (16bits)
    1. 0b0100000110101101
    1. 0b0101100011001010
    1. 0b0001001001101110
    1. 0b1001010000100101
    1. 0b1000001101010110
    1. 0b1101010101101110
    1. 0b1010010001101110
    1. 0b0100100101011100
    1. 0b1011100110011010
    1. 0b0100010011011101

1. Escribir un programa en C que utilizando *printf* y *scanf* resuelva el
   ejercicio anterior. El número debe ser ingresado en formato
   *0b0100010011011101*.

   > Hint: a falta de un formato específico para leer e imprimir números
   > binarios, escribir primero una función que permita obtener el número
   > representado en un string de 1s y 0s.

1. Escribir un programa en C que identifique el formato del número ingresado e
   imprima la representación de ese número en decimal, hexadecimal y binario.

1. Escribir un programa en C que imprima el tamaño de los siguientes tipos:
   *int*, *unsigned int*, *unsigned long int*, *char*, *char \**, *float*,
   *double*, *float \**, *double \**, y *unsigned int \**. Compilar el programa
   para una arquitectura de 32bits y una de 64bits para ver la diferencia.

   > Hint:
   >
   > $ gcc -Wall -m32 programa.c -o programa_32.c
   >
   > $ gcc -Wall -m64 programa.c -o programa_64.c

1. Escribir un programa en C que muestre el _endianness_ de la plataforma en la
   que se ejecuta el programa.

   > Hint: read the book

1. Utilizar la herramienta qemu para ejecutar el programa en distintas
   arquitecturas.

   > Hint: pueden instalar las herramientas qemu-user-static gcc gcc-multilib-sparc64-linux-gnu
   > o utilizar el dockerfile incluido en esta práctica.
   >
   > $ gcc print_endianness.c --static -o print_endianness_x86_64
   >
   > $ ./print_endianness_x86_64
   >
   > $ sparc64-linux-gnu-gcc print_endianness.c --static -o print_endianness_sparc
   >
   > $ qemu-sparc64-static print_endianness_sparc
   >

1. Resolver los siguientes problemas de álgebra booleana.
    1. (~A) para:
        1. A = 0xac
        1. A = 0x11
        1. A = 0x23
        1. A = 0xde
    1. (A | B)  para:
        1. A = 0xac ; B = 0x32
        1. A = 0x11 ; B = 0xaa
        1. A = 0x23 ; B = 0xff
        1. A = 0xde ; B = 0x13
    1. (A & B)  para:
        1. A = 0xac ; B = 0x32
        1. A = 0x11 ; B = 0xaa
        1. A = 0x23 ; B = 0xff
        1. A = 0xde ; B = 0x13
    1. (A ^ B)  para:
        1. A = 0xac ; B = 0x32
        1. A = 0x11 ; B = 0xaa
        1. A = 0x23 ; B = 0xff
        1. A = 0xde ; B = 0x13

1. Escribir un programa en C que utilizando *printf* y *scanf* resuelva el
   ejercicio anterior. Los números deben ser ingresados por separado en formato
   *0x1234*.

1. Resolver los siguientes problemas de manejo de bits.
    1. (0xffe2 >> 3)
    1. (0xace2 << 5)
    1. (0x12e2 >> 2)
    1. (0xf1eb >> 1)
    1. (0xab12 << 6)
    1. (0x62ea >> 2)

1. Escribir una función en C que aproveche las operaciones de bits para setear
   (poner en 1) o clearear (poner en 0) un bit específico (index: 0, 1, 2, ...)
   dentro de una variable de 32bits. La variable modificada es devuelta por
   return de la función.

   ```c
   uint32_t set_bit_on_var(uint32_t var, size_t index);
   ```

1. Escribir en representación entera de 16bits con complemento a dos los
   siguientes números.
    1. 14772
    1. 12110
    1. -13483
    1. -8104
    1. 11518
    1. -29641
    1. -3188
    1. -19378
    1. 8566
    1. -4682

1. Convertir la siguiente representación binaria de 16bits a decimal,
   suponiendo primero que es una representación entera sin signo, luego una
   representación entera con signo en complemento a dos y finalmente una en
   complemento a uno.
    1. 0b1111000010010011
    1. 0b0011110100011101
    1. 0b1010011011010111
    1. 0b0110101001010111
    1. 0b1111001101000001
    1. 0b0100110000011011
    1. 0b1111001101001000
    1. 0b0110001100000011
    1. 0b1011101001101011
    1. 0b0100111110011011

1. Escribir una función en C que acepte por parámetro un número entero sin
   signo e imprima la representación entera con signo y sin signo. Probar la
   función con los siguientes números.
    1. 53888
    1. 47428
    1. 36650
    1. 1455
    1. 29128
    1. 36040
    1. 65536
    1. 52854
    1. 29626
    1. 46818

1. Asumiendo que las siguientes expresiones son evaluadas en una arquitectura
   de 32bits que utiliza aritmética en complemento a dos, resolver a que evalúan.
   1. `-2147483647-1 == 2147483648U`
   1. `-2147483647-1 < 2147483647`
   1. `-2147483647-1U < 2147483647`
   1. `-2147483647-1 < -2147483647`
   1. `-2147483647-1U < -2147483647`
   1. `2147483647U > -2147483647-1`
   1. `2147483647 > (int) 2147483648U`
   1. `-1 < 0U`
   
   > Hint: escribir un programa en C que compruebe los resultados.

1. Escribir una función en C que tome como parámetro un número entero de 16bits
   con signo (*short int*), copie el valor a una variable de 32bits (*int*) e
   imprima su valor. Escribir un programa que utilice esta función y la escrita
   anteriormente que imprime la representación en memoria de la variable para
   ver cómo cambia en distintas arquitecturas utilizando como entrada los
   siguientes números.

   > Hint: utilizar qemu-sparc64-static para ejecutar el programa en
   > arquitecturas big-endian
    1. 13528
    1. -11674
    1. 27091
    1. -15913
    1. 22782
    1. -8521
    1. 4874
    1. -698
    1. 13992
    1. 17396

1. Escribir una función en C que tome como parámetro un número entero de 32bits
   con signo (*int*), copie el valor a una variable de 32bits (*short int*) e
   imprima su valor. Escribir un programa que utilice esta función y la escrita
   anteriormente que imprime la representación en memoria de la variable para
   ver cómo cambia en distintas arquitecturas.

   > Hint: utilizar qemu-sparc64-static para ejecutar el programa en
   > arquitecturas big-endian
    1. -1580948425
    1. 1870865340
    1. -107982815
    1. -157511958
    1. 742922907
    1. -1163069406
    1. 1813815629
    1. 223375263
    1. -625813639
    1. 403361717

1. Calcular la suma de las siguientes variables contra sí mismas suponiendo que
   son resueltas en una arquitectura de 32bits que utiliza una aritmética de
   complemento a dos (*uint32_t*). Indicar los casos en los que el resultado no es válido.
    1. 888678457
    1. 2851757120
    1. 1912450232
    1. 4079538690
    1. 4154371837
    1. 1988670315
    1. 442559150
    1. 2595390421
    1. 2860812492
    1. 515237114


1. Calcular la suma de las siguientes variables contra sí mismas suponiendo que
   son resueltas en una arquitectura de 32bits que utiliza una aritmética de
   complemento a dos (*int32_t*). Indicar los casos en los que el resultado no es válido.
    1. 9837
    1. 18328
    1. 30932
    1. -26481
    1. -24356
    1. 2260
    1. 25312
    1. -31865
    1. 4919
    1. -336

1. Escribir un programa en C que permita ingresar un número y resuelva los dos
   ejercicios anteriores. En caso de ser positivo calcular la suma tanto para
   una representación de *uint32_t* como para una representación *int32_t*.

1. Dadas las definiciones *int a, b;* y teniendo en cuenta que los enteros
   signados se representan en complemento a dos. Además, que las constantes
   *INT_MIN* e *INT_MAX* representan los valores mínimo y máximo que puede
   tener un entero de 32 bits, y la constante *W = 31*. Una las distintas
   descripciones con sus respectivas expresiones.

   * Descripciones:
        1. `~a` (complemento a uno)
        1. `a`
        1. `a * 7`
        1. `(a < 0) ? 1 : -1`
   * Expresiones:
        1. `~(~a | (b ^ (INT_MIN + INT_MAX)))`
        1. `((a ^ b) & ~b) | (~(a ^ b) & b)`
        1. `1 + (a << 3) + ~a`
        1. `(a << 4) + (a << 2) + (a << 1)`
        1. `((a < 0) ? (a + 3) : a) >> 2`
        1. `a ^ (INT_MIN + INT_MAX)`
        1. `~((a | (~a + 1)) >> W) & 1`
        1. `~((a >> W) << 1)`
        1. `a >> 2`

1. Convertir los siguientes números en representación decimal a binario de
   16bits con punto fijo (1bit parte entera, 7bits parte fraccional). Para cada
   caso indicar el error por representación.
    1. 1.125
    1. 0.6723
    1. 0.98911
    1. 0.25
    1. 0.8984
    1. 0.743
    1. 1.832
    1. 0.902
    1. 0.12300
    1. 1.1111

1. Convertir los siguientes números representados en punto fijo a decimal.
    1. 11.101110
    1. 1101.1111
    1. 0110.1101
    1. 010000.01
    1. 100.10100
    1. 10.101010
    1. 1.1011100
    1. 10001.111
    1. 0.1110010
    1. 1.1000010

1. Convertir las representaciones binarias en punto flotante de 7 bits con 1 bit de signo, 3 bits de exponente y 3 de parte fraccionaria (seeefff) a sus valores numéricos fraccionarios.

    1. 0b1111101
    1. 0b0110101
    1. 0b0000110
    1. 0b1110000
    1. 0b1100100
   
   > Hint: identificar primero a qué caso de representación de punto flotante simil IEEE representan (valores normalizados, denormalizados, especiales).

1. Escribir un programa en C que permita realizar la identificación del caso de punto flotante para un valor con una codificación de 7 bits (seeefff). Basta *simplemente* con identificar los casos e imprimir mensajes utilizando *printf* indicando el caso correspondiente.

1. Hallar las representaciones binarias en punto flotante de 7 bits con 1 bit de signo, 4 bits de exponente y 4 de parte fraccionaria (seeeeffff) y luego sus valores numéricos en base 10.

    1. Denormalizado menor
    1. Normalizado mayor
    1. NaN
    1. Infinito positivo
    1. Cero negativo

1. Convertir los siguientes valores numéricos a su representación en punto flotante de 7 bits con 1 bit de signo, 3 bits de exponente y 3 de parte fraccionaria (seeefff).

    1. 15.0
    1. NaN
    1. -4.25
    1. -0.125
    1. 6.75
    1. 0.0
    1. 1.0
    1. -∞
    1. 14.4

   > Hint: identificar primero e, E, 2^E, bias, f, M y verificar cumplimiento de v = (-1)^s * M * 2^E.

1. Resolver a qué evalúan las siguientes expresiones de C y justificar por qué.
Los valores de las variables x, f y d son arbitrarios y sus tipos son respectivamente int, float y double. Además, f y d no pueden ser +∞, −∞ ni NaN.

   1. `f == -(-f)`
   1. `x == (short) (float) x`
   1. `(d + f) - d == f`
   1. `f == (float) (double) f`
   1. `3.0/5.0 == 3/5.0`
   1. `d > f ⇒ -f > -d`
   1. `d == (double) (float) d;`
   
   > Hint: escribir un programa en C que compruebe los resultados.
