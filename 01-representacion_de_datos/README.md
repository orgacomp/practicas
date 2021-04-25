01 - Representación de datos
============================

El objetivo de esta practica es ganar agilidad en la conversión de números *a
ojo* y saber como utilizar código C para no perder la cabeza. La conversión *a
ojo* suele ser muy útil en el momento de leer código asembler ya que en general
los números estarán representados en hexadecimal o en binario. 

1. Convertir los siguientes números en representación decimal a binario (8bits)
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
    1. 0cubo143
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

