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

### La herramienta `cmake`
[CMake](https://es.wikipedia.org/wiki/CMake)
es lo que se conoce como un sistema de metaconstrucción. 
No se utiliza para construir (generar, *build* en inglés) el programa ejecutable de una aplicación sino
que genera archivos de proyecto nativos para la plataforma de destino. 
Por ejemplo, CMake en Windows producirá una solución para Visual Studio; 
en Linux producirá un fichero Makefile; 
en macOS producirá un proyecto para XCode y así sucesivamente. 
Eso es lo que la palabra meta significa: CMake construye sistemas de construcción 
(*builders*). 
La herramienta make es un sistema de construcción, posiblemente el más ubicuo.

Un proyecto basado en CMake siempre contiene un fichero `CMakeLists.txt`. 
Este fichero de texto describe cómo se estructura el proyecto, la lista de ficheros 
de código fuente que se ha de compilar, lo que CMake debe generar a partir de él y así sucesivamente. 
Se trata en definitiva de un fichero de configuración para la herramienta CMake.
CMake leerá las instrucciones del fichero y producirá el resultado deseado. 

Una característica positiva de CMake es el llamado "out-of-source build". 
Cualquier fichero requerido para la construcción final, incluyendo los ejecutables, 
será almacenado en un directorio de construcción separado (usualmente llamado build/). 
Esto evita que el directorio de origen que contiene el código fuente se llene de 
ficheros no deseados y hace que sea fácil volver a empezar: sólo hay que eliminar 
el directorio destino de la compilación y listo.

CMake es una herramienta muy potente que admite multitud de opciones.
En 
[la documentación](https://cmake.org/cmake/help/latest/index.html) 
de la herramienta se pueden estudiar en profundidad estas opciones, pero para la utilización que perseguimos
realizar en esta asignatura bastará con que estudie detenidamente 
[este breve tutorial](https://www.internalpointers.com/post/modern-cmake-beginner-introduction).

En el directorio raíz del repositorio de esta práctica hallará un subdirectorio `fibonacci_sum` con el
siguiente contenido:

```
  fibonacci_sum
  ├── build                      // Directorio de 'construcción' de la aplicación
  ├── CMakeLists.txt             // Fichero de configuración para CMake
  ├── doc                        // Documentación
  ├── fibonacci.Doxyfile         // Fichero de configuración para Doxygen
  ├── LEE_ME.txt
  ├── lib                        // Librerías
  └── src                        // Código fuente de la aplicación
      ├── fibonacci_main.cc
      ├── fibonacci_sum.cc
      ├── fibonacci_sum.h
      ├── tools.cc
      └── tools.h
```
Esa estructura de directorios es habitual en muchos proyectos de desarrollo de software.
En este ejemplo se ha tomado la aplicaciĺn `fibonacci_sum` que calcula la suma de términos pares de la serie
de Fibonacci y se ha fragmentado la aplicación en 5 ficheros de código (`*.cc` y `*.h`).
El fichero de configuración `CMakeLists.txt` contiene la configuración que se utiliza para el despliegue de la
aplicación.
Al efecto de ilustrar este proceso, el proyecto crea una librería `libtools.a` que aloja en el directorio `lib`. 
El programa binario (`fibonacci_sum`) se construye enlazando esta librería con el resto del código objeto
producto de la compilación.

### Entorno de trabajo
Al realizar los siguientes ejercicios cree dentro de su repositorio de esta práctica un directorio diferente
para cada uno de los ejercicios (proyectos).
Tómese como ejemplo el primero de los ejercicios.
Ponga a cada uno de esos directorios nombres significativos (fechas, complejos, racionales por ejemplo).

Haga que cada uno de sus programas conste de 3 ficheros:
* Un fichero `fechas.cc` (programa principal) que contendrá la función `main` e incluirá el fichero de cabecera `fecha.h`
* El fichero `fecha.h` que contendrá las declaraciones correspondientes a la clase `Fecha`.
* El fichero `fecha.cc` que contendrá el código (definiciones) correspondientes a la clase `Fecha`.
* Obviamente si el programa principal (`fechas.cc`) utiliza otras clases, debería incluir (`#include`) los
  correspondientes ficheros de cabecera.
Modifique estos nombres de ficheros para adaptarlos al ejercicio en cuestión.

La compilación del programa correspondiente a cada ejercicio se automatizará con un fichero `CMakeLists.txt`
que se utilizará con `cmake`.

Así pues, la estructura de ficheros y directorios correspondiente a uno de los ejercicios (fechas, p. ej)
sería la siguiente:
```
fechas
    ├── build           // Directorio inicialmente vacío para alojar el programa ejecutable
    ├── CMakeLists.txt  // Fichero de configuración para cmake
    └── src             // Directorio contenedor del código fuente del ejercicio
        ├── fecha.cc
        ├── fecha.h
        └── fechas.cc
```

Desarrolle cada uno de estos ejercicios de forma incremental, probando cada una de las funciones que va Ud.
desarrollando. Utilice el depurador de VSC para corregir cualquier tipo de error semántico que se produzca en
cualquiera de sus desarrollos.

### Ejercicios
1. La clase Fecha.

Desarrolle una clase `Fecha` que permita representar y gestionar fechas.
Incorpore en la clase los miembros de datos y métodos que considere adecuados para la finalidad que se
persigue en este ejercicio.
Incluya un método o función que permita determinar si el año correspondiente a una fecha es un año bisiesto o
no.
Realice un programa cliente `fechas.cc` que tome como parámetro una fecha, un número y un nombre de fichero:
```
./fechas
Modo de uso: ./fechas dd/mm/aa N fichero_salida.txt
Pruebe ./fechas --help para más información
```
El programa deberá imprimir en el fichero de salida (tercer parámetro) las N (segundo parámetro) fechas cronológicamente posteriores a la
introducida (primer parámetro) con una separación de un día entre fechas sucesivas.

2. La clase Complejo.

Todo
[número complejo](https://es.wikipedia.org/wiki/N%C3%BAmero_complejo)
puede representarse como la suma de un número real y un número imaginario, de la forma `a + bi` donde el
término `a` es la parte real, `b` la parte imaginaria e `i` la
[unidad imaginaria](https://es.wikipedia.org/wiki/Unidad_imaginaria).

En este ejercicio se propone desarrollar una clase `Complejo` que permita operar con números complejos.

Separe el diseño de su clase `Complejo` en dos ficheros, `complejo.h` y `complejo.cc` conteniendo
respectivamente la declaración y la definición de la clase.
Siga las indicaciones del tutorial 
[Class code and header files](https://www.learncpp.com/cpp-tutorial/89-class-code-and-header-files/)
para realizar esta separación de su clase en dos ficheros.

Desarrolle un programa cliente `complejos.cc` que permita operar con números complejos y haga uso
de la clase `Complejo` que diseñe.
La clase `Complejo` ha de contener al menos métodos que permitan (*print()*) imprimir un número 
complejo así como sumar (*Add()*) y restar (*Sub()*) números complejos.
Así la función *main* del programa `complejos.cc` podría contener sentencias como las siguientes:

```
main() {
  Complex c1{4, 5}, c2{7, -8};
  Complex resultado;
  resultado = add(n1,n2);
  resultado.print();
  resultado = sub(n1,n2);
  resultado.print();
}
```
que imprimirían en pantalla los resultados de las dos operaciones consignadas.

Incluya (libremente) cualesquiera otras operaciones que considere adecuado incluir como métodos en la clase
`Complejo`.


3. La clase Racional.

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
* La clase `Racional` que incluirá al menos métodos para:
    * Crear objetos de tipo `Racional`. Se debe implementar un constructor por defecto y uno parametrizado.
    * Escribir (a fichero o a pantalla) un objeto de tipo `Racional`.
    * Leer (por teclado o desde fichero) un objeto de tipo `Racional`.
* El programa `racionales.cc` ha de contar con funciones que permitan:
    * Sumar dos objetos de tipo `Racional`.
    * Restar dos objetos de tipo `Racional`.
    * Multiplicar dos objetos de tipo `Racional`.
    * Dividir dos objetos de tipo `Racional`.
    * Comparar objetos de tipo `Racional`.
		Estas funciones debieran desarrollarse como métodos de la clase, aunque como primera aproximación pueden
		desarrollarse como funciones ordinarias externas a la clase.
* El programa ha de permitir leer un fichero de texto en el que figuran pares de números racionales
separados por espacios de la forma:

```
a/b c/d
e/f g/h
  ...
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

Si el programa se ejecuta pasando como parámetro la opción `--help` se ha de obtener:

```
./racionales -- Números Racionales
Modo de uso: ./racionales fichero_entrada fichero_salida 

fichero_entrada: Fichero de texto conteniendo líneas con un par de números racionales: `a/b c/d` separados por un espacio
fichero_salida:  Fichero de texto que contendrá líneas con las operaciones realizadas: `a/b + c/d = n/m`
```






### Referencias
* [CMake](https://es.wikipedia.org/wiki/CMake)
* [Introduction to modern CMake for beginners](https://www.internalpointers.com/post/modern-cmake-beginner-introduction)
* [Números complejos](https://es.wikipedia.org/wiki/N%C3%BAmero_complejo)
* [Rational Number](https://en.wikipedia.org/wiki/Rational_number)
*	[Class code and header files](https://www.learncpp.com/cpp-tutorial/89-class-code-and-header-files/)
* [Doxygen](https://en.wikipedia.org/wiki/Doxygen)
* [Documenting C++ Code](https://developer.lsst.io/cpp/api-docs.html)
* [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)
