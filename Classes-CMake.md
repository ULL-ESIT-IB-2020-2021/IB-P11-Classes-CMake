# Práctica 11. Introducción a la Programación Orientada a Objetos. CMake.

### Objetivos
Los objetivos de esta práctica son que el alumnado:
* Desarrolle programas sencillos en C++ que utilicen clases, así como todas las características del lenguaje
  estudiadas
* Aloje todo el código fuente de sus programas en repositorios privados de GitHub
* Sepa depurar sus programas usando la interfaz de depuración del VSC
* Incluya en sus programas comentarios en el formato requerido por Doxygen
* Conozca la herramienta CMake y sepa usarla para construir sus programas ejecutables

### Rúbrica de evaluacion de esta práctica
Se señalan a continuación los aspectos más relevantes (la lista no es exhaustiva)
que se tendrán en cuenta a la hora de evaluar esta práctica:
* El alumnado ha de acreditar conocer los conceptos expuestos en el material de referencia de esta práctica.
* El alumnado ha de acreditar que ha realizado todos los ejercicios propuestos, así como ser capaz de desarrollar otros similares.
* Ha de acreditar que es capaz de escribir un fichero Makefile para automatizar el proceso de compilación de sus programas.
* El código que escriba ha de estar escrito de acuerdo a los estándares definidos en la Guía de Estilo de Google para C++.
* Todos los identificadores que utilice en su programa (constantes, variables, etc.) deberán ser
  siempre significativos. No utilice nunca identificadores de una única letra, tal vez con la excepción de las
  variables que utilice para iterar en un bucle.
* Antes de su ejecución, todos los programas que desarrolle, deben imprimir en pantalla un
  mensaje indicando la finalidad del programa así como la información que precisará del usuario para su correcta ejecución.
* Ante la presencia de cualquier bug, el alumnado ha de conocer las técnicas básicas de depuración usando VSC
* Todos los ficheros de código del proyecto correspondiente a esta práctica han de alojarse en un repositorio
  de GitHub
* Los programas deben contener comentarios adecuados en el formato requerido por Doxygen
* Los programas deben estructurarse en directorios diferentes para cada "proyecto" y hacer que cada uno de
  ellos contenga un fichero `CMakeLists.txt` con la configuración de despliegue del proyecto.

### Introducción a la criptografía


### Entorno de trabajo
Al realizar los siguientes ejercicios cree dentro de su repositorio de esta práctica un directorio diferente
para cada uno de los ejercicios (proyectos).
Tómese como ejemplo el primero de los ejercicios:

Ponga a cada uno de esos directorios nombres significativos.
Haga que cada uno de sus programas conste de 3 ficheros:
* Un fichero `mi_programa.cc` (programa principal) que contendrá la función `main` e incluirá el fichero de cabecera `funciones.h`
* El fichero `funciones.h` que contendrá las declaraciones de las diferentes funciones que se utilizan en el
  programa principal para resolver el ejercicio en cuestión.
* El fichero `funciones.cc` que contendrá el código (definiciones) de las funciones declaradas en el fichero
  de cabecera.

Modifique los nombres de los ficheros que aquí se proponen para adaptarlos al ejercicio en cuestión.

La compilación de los programas correspondientes a cada ejercicio se automatizará con un fichero Makefile para
cada ejercicio.

Desarrolle cada uno de estos ejercicios de forma incremental, probando cada una de las funciones que va Ud.
desarrollando. Utilice el depurador de VSC para corregir cualquier tipo de error semántico que se produzca en
cualquiera de sus desarrollos.

#########

Haga que el proyecto correspondiente a esta práctica conste al menos de 3 ficheros:
* Un fichero `cripto.cc` (programa principal) que contendrá la función `main` e incluirá el fichero de cabecera `funciones_cripto.h`
* El fichero `funciones_cripto.h` que contendrá las declaraciones de las diferentes funciones que se utilizan en el
  programa principal.
* El fichero `funciones_cripto.cc` que contendrá el código (definiciones) de las funciones declaradas en el fichero
  de cabecera.

La compilación del programa ha de estar automatizada mediante un fichero Makefile.

Desarrolle su programa de forma incremental, probando cada una de las funciones que va Ud.
desarrollando. Utilice el depurador de VSC para corregir cualquier tipo de error semántico que se produzca en
cualquiera de sus desarrollos.

### Ejercicios
1.  La clase Racional
Un 
[número racional](https://en.wikipedia.org/wiki/Rational_number)
tiene un numerador y un denominador de la forma `p/q` donde `p` es el numerador y `q` el denominador.
Por ejemplo, 1/3, 3/4 y 10/4 son números racionales.

Un número racional no puede tener denominador 0, pero sí puede ser cero el numerador.
Todo número entero `n` es equivalente al racional `n/1`.
Los números racionales se utilizan en cálculos precisos que involucran fracciones.
Por ejemplo, `1/3 = 0.33333 ...`.
Este número no puede ser representado de forma precisa en formato de punto flotante utilizando los tipos float o double.
Para obtener resultados precisos es conveniente usar números racionales.

C++ dispone de tipos de datos para enteros y números en punto flotante, pero no para racionales.
En este ejercicio se propone el diseño de una clase para representar números racionales.

Desarrolle un programa cliente `racionales.cc` que permita operar con números racionales y haga uso
de la clase `Racional` que ha de diseñarse.

Las siguientes deben tomarse como especificaciones del programa a desarrollar:
* Separe el diseño de su clase `Racional` en dos ficheros, `racional.h` y `racional.cc` conteniendo
  respectivamente la declaración y la definición de la clase.
  Siga las indicaciones del tutorial 
	[Class code and header files](https://www.learncpp.com/cpp-tutorial/89-class-code-and-header-files/)
  para realizar esta separación de su clase en dos ficheros.
* La clase `Racional` que incluirá al menos métodos para:
    * Crear objetos de tipo `Racional`. Se debe implementar un constructor por defecto y uno parametrizado.
    * Escribir (a fichero o a pantalla) un objeto de tipo `Racional`.
    * Leer (por teclado o desde fichero) un objeto de tipo `Racional`.
    * Sumar dos objetos de tipo `Racional`.
    * Restar dos objetos de tipo `Racional`.
    * Multiplicar dos objetos de tipo `Racional`.
    * Dividir dos objetos de tipo `Racional`.
    * Comparar objetos de tipo `Racional`.
* El programa ha de permitir leer un fichero de texto en el que figuran pares de números racionales
separados por espacios de la forma:

```
a/b c/d
e/f g/h
```

y para cada par de números racionales, el programa ha de imprimir en otro fichero de salida todas las operaciones posibles
con cada uno de los pares de números del fichero de entrada, de la forma:

```
a/b + c/d = n/m
...
```

Si el programa se ejecuta sin pasar parámetros en la línea de comandos, debemos obtener el siguiente mensaje:

```
./racionales -- Números Racionales
Modo de uso: ./racionales fichero_entrada fichero_salida
Pruebe ./racionales --help para más información
```

Si el programa se ejecuta pasando la opción `--help` se ha de obtener:

```
./racionales -- Números Racionales
Modo de uso: ./racionales fichero_entrada fichero_salida 

fichero_entrada: Fichero de texto conteniendo líneas con un par de números racionales: `a/b c/d` separados por un espacio
fichero_salida:  Fichero de texto que contendrá líneas con los números operados: `a/b + c/d = n/m`
```



2. La clase Complejo

3. La clase Fecha

4. La clase Matriz
https://stackoverrun.com/es/q/422606
https://www.quantstart.com/articles/Matrix-Classes-in-C-The-Header-File/





### Referencias
* [Rational Number](https://en.wikipedia.org/wiki/Rational_number)
*	[Class code and header files](https://www.learncpp.com/cpp-tutorial/89-class-code-and-header-files/)
* [Doxygen](https://en.wikipedia.org/wiki/Doxygen)
* [Documenting C++ Code](https://developer.lsst.io/cpp/api-docs.html)
* [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
