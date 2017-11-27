# Debug

En esta carpeta hay cuatro archivos Aquí hay cuatro carpetas, cada una
con sus ejercicios. Las respuestas a los ejercicios tienen que estar
en esta carpeta, bajo el nombre `respuestas.md`.

## Varios bugs

En la carpeta `bugs/` hay varios bugs ya hechos y resueltos, pensado
para hacerlo en clase. Aquí tenemos un `Makefile` donde, además,
usamos una nueva variable: `$CFLAGS`. En esa variable pueden poner los
distintos flags de compilación que quieran pasarle a `$CC`. Esta
carpeta ya tiene un `Makefile` hecho, que compila todos los
casos. Algunas cosas que pueden hacer es:

- Correr el programa con un debugger, sin agregar flags de
debug. ¿Tienen toda la información que requerían?

No, nos falta información acerca del error del programa.

- ¿Qué pasa si ponen el flag de debug? ¿Qué flag de optimización es el
mejor para debuggear?

El mejor es O0 y O1 porque ambos describen el error.Con O1 por ejemplo, el mensaje es el siguiente: 

Program received signal SIGSEGV, Segmentation fault.
0x00005555555546c3 in add_array ()

- Agreguen algún flag para que informe todos los warnings en la
compilación, como `-Wall`. ¿Alguno les da alguna pista de por qué el
programa se rompe?

El flag -Wall no da más información. Probé con el flag -g O0, el cual informa un error de sintaxis en la línea 19 del código del programa. El mensaje es el siguiente: 

at add_array_segfault.c:19

19          b[i] = i;

#Floating point exception

En la carpeta `fpe/` hay tres códigos de C, independientes, para
compilar.  Cada uno de estos códigos genera un ejecutable. Hay además
una carpeta que define la función `set_fpe_x87_sse_`. Una vez
compilados los tres ejecutables sin la opción `-DTRAPFPE`, responder
las siguientes preguntas:

- ¿Qué función requiere agregar `-DTRAPFPE`? ¿Cómo pueden hacer que el
programa *linkee* adecuadamente?
- Para cada uno de los ejecutables, ¿qué hace agregar la opción
`-DTRAPFPE` al compilar? ¿En qué se diferencian los mensajes de salida
de los programas con y sin esa opción cuando tratan de hacer una
operación matemática prohbida, como dividir por 0 o calcular la raíz
cuadrada de un número negativo?

Nota: Si agregan `-DTRAPFPE`, el programa va a tratar de incluir, en
la compilación, un archivo `.h` que está en la carpeta
`fpe_x87_sse`. Para pedirle al compilador que busque archivos `.h` en
una carpeta, usen el flag `-Icarpeta` (sí, sin espacio en el medio).

Otra nota: Para poder linkear `fpe_x87_sse.c` tienen que agregar la
librería matemática `libm`, con `-lm`.


## Segmentation Fault

En la carpeta `sigsegv/` hay códigos de C y de FORTRAN con su
`Makefile`.  Compilen y corran `small.e` y `big.e`.  Identifiquen los
errores que devuelven (¡si devuelven alguno!) los ejecutables.  Ahora
ejecuten `ulimit -s unlimited` en la terminal y vuelvan a
correrlo. Luego responder las siguientes preguntas:

- ¿Devuelven el mismo error que antes? 

Al correr el programa big.e la terminal muestra el error "segmentation fault".
Al ejecutar "ulimit -s unlimited" el programa tarda en correr. 

- Averigüen qué hicieron al ejecutar la sentencia `ulimit -s
unlimited`. Algunas pistas son: abran otra terminal distinta y fíjense
si vuelve al mismo error, fíjense la diferencia entre `ulimit -a`
antes y después de ejecutar `ulimit -s unlimited`, googleen, etcétera.

Lo que hicimos fue agrandar el espacio para las variables del programa en el stack de memoria. 

- La "solución" anterior, ¿es una solución en el sentido de debugging?

No es una solución óptima porque no es cómoda para el usuario. 

- ¿Cómo harían una solución más robusta que la anterior, que no
requiera tocar los `ulimits`?

La solución sería que la asignación de memoria sea en el heap, es decir que sea dinámica y no estática. 

## Valgrind

En la carpeta `valgrind/` hay ejemplos en C y FORTRAN que se pueden
ejecutar con valgrind. Describan el error y por qué sucede

Al correr Valgrind en el programa test_oob4, devuelve el siguiente error: 

=636== Invalid write of size 4

==636==    at 0x1087FF: mysub (in /home/ctpc17/Desktop/Repositorio/HOdebug-profile/debug/valgrind/C/test_oob4)

==636==    by 0x108865: main (in /home/ctpc17/Desktop/Repositorio/HOdebug-profile/debug/valgrind/C/test_oob4)

==636==  Address 0x0 is not stack'd, malloc'd or (recently) free'd
Invalid write of size 4 at 0x1087FF by 0x108865: 

lo cual interpreto que significa un error de lectura permitida, ya que malloc intenta asignar un bloque de memoria no permitido.  

## Funny

En la carpeta `funny/` hay un código de C. Describan las diferencias
de los ejecutables al compilar con y sin el flag `-DDEBUG`. ¿De dónde
vienen esas diferencias?

Al ejecutar el programa sin el flag el terminal devuelve el mensaje de error "segmentation fault", mientras que al ejecutarlo con el flag el terminal devuelve el mismo error e imprime el mensaje I'm HERE !!!!. Esta técnica es útil para encontrar errores en el programa imprimiendo mensajes. 



