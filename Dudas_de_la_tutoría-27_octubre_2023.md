# Dudas de la Práctica 06/07 (Tutoría 26/27 de octubre)

Le adjunto aquí las dudas que me han surgido durante esta práctica. He aprovechado y creado un archivo .md en GitHub para poder tanto explicar como aplicar mejor lo aprendido en clase.
Así creo que también se podrá visualizar mejor las dudas. Si usted tiene otra preferencia de formato no presencial para futuras tutorías, estaré encantado de cambiar el formato.

## Duda 1 (Práctica 06): Increasing Pairs (Jutge)
En la práctica anterior (24 de octubre), se nos propuso como tercer ejericio el [Increasing Pairs del Jutge (P73501)](https://jutge.org/problems/P73501_en).

El programa que envié fue el que me dio tiempo a desarrollar durante el periodo de prueba, que aún así es muy similar al que le adjunto aquí. ¿En los comprimidos de las prácticas debemos adjuntar los programas tal cual desarrollados en clase o una vez los hayamos resuelto/pulido tras el examen?

En la práctica no tuvimos la posibilidad de que se nos revisara el código, por lo que me he quedado con la duda de por qué mi código no es capaz de resolver el problema:

```cpp
/**
  * Universidad de La Laguna
  * Escuela Superior de Ingeniería y Tecnología
  * Grado en Ingeniería Informática
  * Informática Básica 2023-2024
  *
  * @file increasing_pairs.cc
  * @author Francisco Gabriel Ruiz Ruiz
  * @date Oct 24 2023
  * @brief The program reads sequences of natural numbers, and for each
  *        one it prints the number of pairs of consecutive numbers such that
  *        the second number of the pair is greater than the first one.
  * @bug The program currently does not work.
  * @see https://jutge.org/problems/P73501_en
  * @contact alu0101618586@ull.edu.es
  */

#include <iostream>
#include <vector>

int main() {
  int user_input{0};
  std::vector<int> sequence_of_numbers;

  // The program reads an indefinite amount of user_inputs and stores
  // them in a vector
  while (std::cin >> user_input) {
    sequence_of_numbers.emplace_back(user_input);
    }   

  int bigger_pair_counter{0};
  // Compares the numbers in the vector that are one next to the other
  for (int sequence_counter{0}; sequence_counter != sequence_of_numbers.size(); sequence_counter + 1) {
    if (sequence_of_numbers[sequence_counter] < sequence_of_numbers[(sequence_counter + 1)]) {
      ++bigger_pair_counter;
    }     
  }

  // Prints how many numbers it found that were smaller than the number
  // positioned after them in the vector
  std::cout << bigger_pair_counter << '\n';
  return 0;
}
```
La única manera que se me ocurrió para atacar el problema fue usar un vector en el que almacenara los dígitos introducidos por el usuario, para luego ir comparándolos por parejas.

## Duda 2 (Práctica 07): Resolución de ejercicios propuestos para entregar
En la práctica 07, se adjuntan unos cinco problemas que se recomienda resolver haciendo uso de funciones y la guía de estilo de Google de C++. No tengo claro si se busca que los problemas resueltos se estructuren casi completamente en funciones, incluso si estas resultarían en apenas un par de líneas de código. Le adjunto a continuación unos ejemplos de mis dudas.

En este ejemplo, `sum_of_digits.cc` dada la simpleza del programa, no tuve claro si dividirlo en varias funciones:
```cpp
/**
 * Universidad de La Laguna
 * Escuela Superior de Ingeniería y Tecnología
 * Grado en Ingeniería Informática
 * Informática Básica 2023-2024
 *
 * @file sum_of_digits.cc
 * @author Francisco Gabriel Ruiz Ruiz
 * @date Oct 27 2023
 * @brief The program reads several numbers and prints the sum of the digits
 *        of each one.
 * @bug There are no known bugs
 * @see https://jutge.org/problems/P33839_en
 * @see https://github.com/IB-2023-2024/P07-iterations/blob/main/iterations.md
 * @contact alu0101618586@ull.edu.es
 */

#include <iostream>
#include <vector>
 
int main(int argc, char *argv[]) {
    // Program exits when more than 1 value is entered
    if (argc != 2) {
      std::cerr << "Introduzca un solo valor tras ejecutar el programa." << '\n';
      return 1;
    }   
    int user_number = std::stoi(argv[1]);
    int addition_result{0};
    // Loop extracts each integer from the user's number and adds them
    for (int modified_user_number{user_number}; modified_user_number != 0; modified_user_number /= 10) {      addition_result += modified_user_number % 10;
    }     
    std::cout << "La suma de los dígitos de " << user_number << " es " << addition_result << "." << '\n';
  return 0;
}
```


Otro ejemplo donde la simpleza quizás permitiría la falta de funciones, `serie_fibonacci.cc`:
```cpp
/**
  * Universidad de La Laguna
  * Escuela Superior de Ingeniería y Tecnología
  * Grado en Ingeniería Informática
  * Informática Básica 2023-2024
  *
  * @file serie_fibonacci.cc
  * @author Francisco Gabriel Ruiz Ruiz
  * @date Oct 28 2023
  * @brief The program prints the Fibonacci sequence as long as the user inputs
  * @bug There are no known bugs
  * @see https://github.com/IB-2023-2024/P07-iterations/blob/main/iterations.md
  *      (Exercise 2)
  * @contact alu0101618586@ull.edu.es
  */

#include <iostream>

int main(int argc, char* argv[]) {
  // Program aborts if input is unexpected
  if (argc != 2) {
    std::cerr << "Introduzca un solo número natural después del comando" << '\n';
    return 1;
  }

  int user_number_of_repetitions = std::stoi(argv[1]);
  int fibonacci_result{0};
  int prev_fibonacci_operand{0};
  for (int counter{0}; counter <= user_number_of_repetitions; ++counter) {
    switch (counter) {
      // Program prints output for the first two numbers because they are exceptions
      case 0:
        fibonacci_result = 0;
        std::cout << fibonacci_result;  
        break;
      case 1:
        fibonacci_result = 1;
        std::cout << fibonacci_result;
        break;
      default:
        int store_prev_fibonacci{fibonacci_result};
        fibonacci_result = ((fibonacci_result) + (prev_fibonacci_operand));
        prev_fibonacci_operand = store_prev_fibonacci;
        std::cout << fibonacci_result;
    }
    // Prevents unnecessary spaces and correctly computes when the sequence ends
    if (counter + 1 <= user_number_of_repetitions) {
      std::cout << " ";
    } else {
      std::cout << '\n';
    }
  }
  return 0;
}
```


En este otro, `binary-to-decimal.cc`, intenté estructurarlo más en funciones, aunque no sé si quizás son demasiadas:
```cpp
/**
  * Universidad de La Laguna
  * Escuela Superior de Ingeniería y Tecnología
  * Grado en Ingeniería Informática
  * Informática Básica 2023-2024
  *
  * @file binary-to-decimal.cc
  * @author Francisco Gabriel Ruiz Ruiz
  * @date Oct 29 2023
  * @brief The program converts binary numbers to decimals without using
  *        std::string, std::vector or std::array.
  * @bug There are no known bugs
  * @see https://github.com/IB-2023-2024/P07-iterations/blob/main/iterations.md
  *      (Exercise 3)
  * @contact alu0101618586@ull.edu.es
  */

#include <iostream>
#include <cmath>
#include <cstdlib>

int getBinaryNumberSize(int user_binary_number) {
  int binary_number_size {1};
  if (user_binary_number == 0) {
    binary_number_size = 1;
  } else {
    for (int division_counter{1}; user_binary_number > 1; ++division_counter) {
      user_binary_number /= 10;
      ++binary_number_size;
    }
  }
  return binary_number_size;
}

void checkValidInput(int user_number) {
  for (int counter{0}; user_number != 0; ++counter) {
    if ((user_number % 10 != 0) && (user_number % 10 !=1)) {
      std::cerr << "Introduzca un número binario válido tras ejecutar el comando." << '\n';
      std::exit(2);
    }
    user_number /= 10;
  }
}

int convertFromBinaryToDecimal(int user_number, int binary_number_size) {
  int conversion_result{0};
  for (int binary_exponent_counter{0}; binary_exponent_counter <= binary_number_size; ++binary_exponent_counter) {
    conversion_result += ((pow(2, binary_exponent_counter)) * (user_number % 2));
    user_number /= 10;
  }
  return conversion_result;
}

int main(int argc, char* argv[]) {
  // Program aborts is user input is unexpected
  if (argc != 2) {
    std::cerr << "Introduzca un solo número binario tras ejecutar el comando." << '\n';
    return 1;
  }
  char* user_binary_string = argv[1];
  int user_binary_number = std::atoi(user_binary_string);
  checkValidInput(user_binary_number, binary_number_size);
  int binary_number_size = getBinaryNumberSize(user_binary_number);
  int user_decimal_result{convertFromBinaryToDecimal(user_binary_number, binary_number_size)};
  std::cout << user_decimal_result << '\n';
  return 0;
}
```
En el resto de programas que desarrollé, por su complejidad, sí que usé funciones, pero no estructuré absolutamente todo el contenido del `int main()` en declaraciones de funciones. Mi duda surge principalmente por el ejemplo propuesto en el enunciado de la práctica:
```cpp
 {
  PrintProgramPurpose();
  if (!CheckCorrectParameters(argc, argv, 3)) {
    return 1;
  }
  GetUserInput();
  GetMathematicalOperation();
  GetUserInput();
  CalculateResult();
  PrintResult();

  return 0;
}
```
[Créditos del código](https://github.com/IB-2023-2024/P07-iterations/blob/main/iterations.md)

¿Se podría penalizar por una falta o abuso de funciones en un programa que necesite o no de ellas?

## Duda 3 (Práctica 07): Uso del `int argc, char* argv[]`
En el enunciado de la práctica 07 (el adjuntado anteriormente), se emplea el `int main(int argc, char* argv[])` para el ejercicio. 

Es por ello que en todos los programas de esta práctica implementé esta característica para poder ejecutar comandos como `./binary-to-decimal 101010`. Asimismo, también incluí código para parar el programa si el usuario no introduce el input esperado:
```cpp
// Cabecera del programa...

#include <iostream>

int main(int argc, char* argv[]) {
  // Program aborts is user input is unexpected
  if (argc != 2) {
    std::cerr << "Introduzca un solo número binario tras ejecutar el comando." << '\n';
    return 1;
  }
 // El código continuaría por aquí...
```
En este caso, el programa sale cuando se introduce más de un input (aparte del comando).

Esta función se parece mucho al `std::cin`, aunque le veo un problema que quizás choca con la filosofía de desarrollar programas lo más intuitivos posibles. Esto es porque al lanzar el ejecutable, ya debemos introducir el input junto a él, mientras que con el `std::cin`, lo solíamos acompañar con un `std::cout`explicativo.

¿Debo quitar esto de mis programas, o implementar algo para solucionarlo? Además, ¿debo crear una función para este `if (argc != 2)`, o no es necesario?

## Duda 4 (Práctica 07): Restricción del uso de ciertos statements en los ejercicios
En el ejercicio 3 (`binary-to-decimal.cc`) y 4 (`decimal-to-binary.cc`) se nos restringe el uso de los tipos `std::string`, `std::vector` o `std::array` para desarrollar el ejercicio. Como implementé en todos mis programas la funcionalidad del `int main(int argc, char* argv[])` que le mostré en la duda anterior, me he visto obligado a usar esto en los ejercicios:
```cpp
  char* user_binary_string = argv[1];
  int user_binary_number = std::atoi(user_binary_string);
```
Este código me permite primero identificar qué es lo que busco (el input del usuario, en este caso, se encontraría tras la ejecución del comando, es decir, en la primera posición) para luego convertir ese 'string' en un número con el que pueda trabajar.

Ya que esto no interfiere realmente con el desarrollo posterior de los ejercicios, ¿puedo emplear este método cuando se imponga esta restricción, o debo eliminarlo y prescindir del uso del `int main(int argc, char* argv[])` (o es posible que exista otro método que no recurra a los 'string')?

## Duda 5 (Práctica 07): Presentación de los programas de los ejercicios
Dado que los ejercicios propuestos se han sacado del Jutge, ¿debo ajustar el input y output del código como si fuera a presentárselo al Jutge? No lo tengo claro ya que esto iría en contra del principio de elaborar programas lo más intuitivos que nos sea posibles.

Muchas gracias y un saludo.
