01 - Representación de datos
============================

El objetivo de esta práctica es ganar agilidad en la conversión y trabajo con
números *a ojo* y saber como utilizar código C para no perder la cabeza. La
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

1. Escribir un programa en C que utilizando *printf* y *scanf* resuelva el
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

   > Hint: a falta de un formato especifico para leer e imprimir números
   > binarios, escribir primero una función que permita obtener el número
   > representado en un string de 1s y 0s.

1. Escribir un programa en C que identifique el formato del número ingresado e
   imprima la representación de ese número en decimal, hexadecimal y binario.

1. Escribir un programa en C que imprima el tamaño de los siguientes tipos:
   *int*, *unsigned int*, *unsigned long int*, *char*, *char \**, *float* y
   *double*. Compilar el programa para una arquitectura de 32bits y una de
   64bits para ver la diferencia.

   > Hint:
   >
   > $ gcc -Wall -m32 programa.c -o programa_32.c
   >
   > $ gcc -Wall -m64 programa.c -o programa_64.c

1. Escribir un programa en C que muestre el endianness de la plataforma en la
   que se ejecuta el programa. Ejecutar este programa en distintas

   > Hint: read the book

1. Utilizar la herramienta qemu para ejecutar el programa en distintas arquitecturas.

   > Hint: pueden instalar las herramientas qemu-user-static gcc gcc-multilib-sparc64-linux-gnu
   > o utilizar el dockerfile incluido en esta practica.
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
   ejercicio anterior. Los número deben ser ingresados por separado formato
   *0x1234*.

1. Resolver los siguientes problemas de manejo de bits.
    1. (0xffe2 >> 3)
    1. (0xace2 << 5)
    1. (0x12e2 >> 2)
    1. (0xf1eb >> 1)
    1. (0xab12 << 6)
    1. (0x62ea >> 2)

1. Escribir una función en C que aproveche las operaciones de bits para setear
   (poner en 1) o clerear (poner en 0) un bit especifico (index: 0, 1, 2, ...)
   dentro de una variable de 32bits. La variable modificada es devuelta por
   return de la función.

   ```c
   uint32_t set_bit_on_var(uint32_t var, size_t index);
   ```

1. Escribir en representación entera de 16bit con complemento a dos los
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
   suponiendo primero que es una representación entera sin signo, una
   representación entera con signo en complemento a dos, una representación
   entera con signo en complemento a uno.
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

1. Escribir una función en C que acepte por parámetro un numero entero sin
   signo e imprima la representación entera con signo y sin signo. Testear la
   función con los siguientes número.
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

1. Dadas las definiciones *int a, b;* y teniendo en cuenta que los enteros
   signados se representan en complemento a dos. Además, las constantes
   *INT_MIN* e *INT_MAX* representan los valores mínimo y máximo que puede
   tener un entero de 32 bits, y la constante *W = 31*. Una las
   descripciones de la izquierda con las expresiones de la derecha.

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
