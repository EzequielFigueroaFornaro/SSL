# TP N°1
## Pasos realizados, sus salidas y analisis de cada paso
#### Primer paso - Preprocesar __hello2.c__ incluyendo bibbioleca estandar
 gcc hello2.c  -std=c11 -c -o hello2.i__ 
##### Analisis
- En la  linea 1 del archivoo __hello2.c__ se incluyendo al codico propio (al escribir __#include <------.h>__) la biblioteca deentrada/salida __stdio.h__
- El archivo que crea el preproceso __hello2.i__ contiene: typedef, structs y directivas de la biblioteca que se esta incluyendo. Y final de este se encuentra el codigo propio en el __hello2.c__ sin los comentarios los cuales son removidos y reemplazados por un espacio
#### Segundo paso - Preprocesar __hello3.c__ sin incluir biblioteca estandar
 gcc hello3.c  -std=c11 -c -o hello3.i__ 
##### Analisis
- igual al anterior, pero uso __hello3.c__, la salida __hello3.i__
- A diferencia del __hello2.c__ no se incluye la biblioteca __Stdio.h__, sino que al usar  __printf()__ se refiere al prototipo de la funcion definido por nosotros, el cual indica que la funcion recibe un argumento un puntero a un char (__'const char *s'__) y despues n argumentos más (identificado por __'...'__). 
- El archivo de salida es muy similar al archivo de entrada, ya que no se tiene que no se hace ningun include de una biblioteca estandar, solo el __printf()__ y el __main()__
#### Tercer paso - Compilar __hello3.i__
 gcc hello3.i  -std=c11 -S -o hello3.s__ 
##### Analisis
- Error de compilacion __hello3.i__ : 
    > hello3.c: In function ‘main’:
    > hello3.c:4:1: warning: implicit declaration of function ‘prontf’ [-Wimplicit-function-declaration]
    > prontf("La respuesta es %d\n");
    > ^
    > hello3.c:4:1: error: expected declaration or statement at end of input
- Dice que es un error de sintaxis (falta el cierre del main -> '}')
#### Cuarto paso - Corregir en __hello4.i__ y compilar
 gcc hello4.c -std=c11 -S -o hello4.s__
##### Analisis
- Al compilar devuelve el siguiente warning:
    > hello4.c: In function ‘main’
    > hello4.c:4:1: warning: implicit declaration of function ‘prontf’ [-Wimplicit-function-declaration]
    > prontf("La respuesta es %d\n");
    > ^
- Se pudo realizar la compilación y creación del archivo __hello4.s__. Pero que el prototipo de la función __prontf()__ no se encontró.
- Se ve que traduce del codigo C en lenguaje Assembler, se ve que para poder mostrar el mensaje se realizan las acciones como : MOVL, CALL, etc.
#### Quinto paso - Ensamblar __hello4.o__
 as hello4.s -o hello4.o__
##### Analisis
- Se crea un binario __hello4.o__ el cual genera una traduccion a assemble desde el__hello4.s__ para poder ser entendido por la maquina.
#### Sexto paso - Vincular __hello4.0__ con la biblioteca estandar y genererar ejecutable
 gcc hello4.o -o hello4 -std=c11__
##### Analisis
-Al vincular __hello4.o__ se produce un error error,:
>hello4.o: In function `main':
> hello4.c:(.text+0x1a): undefined reference to `prontf'
> collect2: error: ld returned 1 exit status
el cual no nos deja crear el ejecutable.
- El cual dice que no encuentra la referencia a una funcion llamada __'prontf()'__, ni en el codigo propio,como tampoco en la biblioteca.
#### Septimo paso - Corregir __prontf()__ en __hello5.c__ y generar ejecutable
 gcc hello5.c -o hello5 -std=c11__
##### Analisis
-Al crear el ejecutable nos muestra el sigueinte warning:
> hello5.c: In function ‘main’:
> hello5.c:4:8: warning: format ‘%d’ expects a matching ‘int’ argument [-Wformat=]
> printf("La respuesta es %d\n");
_ El cual nos dice que la funcion __printf()__ esta esperando un argumento mas dado que el __"%d"__ da aentender que se esta esperando un __'int'__
#### Octavo paso - Correr archivo ejectutable __hello5__
 ./hello5__
##### Analisis
- Al ejecutar el archivo nos muestra: 
    > La respuesta es 1219149656
-Como no se le paso el argumento que la funcion esperaba se completo la respuesta con informacion basura.
#### Noveno paso - Corregir en __hello6.c__ y generar ejectutable
 gcc hello6.c -o hello6 -std=c11__
  ./hello6__
##### Analisis
-Crea el ejecutable __hello6__ y se corre, el mismo y muestra el siguiente mensaje: 
    > La respuesta es 42
