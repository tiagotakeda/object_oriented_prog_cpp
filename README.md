# Object Oriented Programming

## Mission

This guide was developed to help members from Skyrats - Autonomous Drones Team from Escola Politécnica da Universidade de São Paulo - to understand the concepts of object oriented programming in C++.

It assumes that the preson who is reading this is already used to programming in C++. If ythis is not your case, please check out the other tutorial about <a href="https://github.com/SkyRats/cpp_workshop">C++ Basic Concepts</a> before following this one.

Since it is a routine for the members to be asked to install Linux (Ubuntu 16.04 LTS) when they enter the team, some instructions are given to be inserted on a Linux Terminal.

If that may be an issue, you can easily follow this guide using an IDE (Codeblocks is a good starting IDE).

## Prerequisites

* **Compilers**:

  * GCC (Linux)

  * MinGW (Windows)

## Contents

1. Definition and Paradigms
2. Concepts
3. Encapsulation
4. Constructors and Destructors
5. Inheritance and Polymorphism
6. Abstract Classes and Multiple Inheritance
7. Defensive Programming
8. Data Persistence
9. Namespace, Templates and Standard Libraries
10. Examples (commented)

## 1 - Definition and Paradigms

Developing software does not envolve only a programming language itself, a good aspect to consider when developing anything is the programming paradigm, or the "way" of programming. 

To be more precise Timothy Budd describes it as "... way of conceptualizing what ist means to preform copmutation, of structuring and organizing how tasks are to be carried out on a computer." in his seminal <a href="https://books.google.com.br/books/about/Multiparadigm_Programming_in_Leda.html?id=qqxQAAAAMAAJ&redir_esc=y">book</a> on multiparadigm programming.

Each language has one or more paradigms. Some examples of paradigms and respective languages:

* Imperative: Pascal and Cobol
* Functional: Lisp, Haskel and Scala
* Logic: Prolog and Datalog
* **Object-Oriented: C++, C#, Java and Python**
* Event-Driven: used mostly in graphcal interfaces
* Declarative: SQL and HTML

In this way, Object Oriented Programming differs from others paradigms because it includes both data and functions. In addition, we are able to create relationships between one object and another.

## Concepts

### ADT - Abstract Data Type

An Abstract Data Type (ADT) is formally defined as a type (or class) for objects whose behavior is defined by a set of value and a set of operations. 

To be more clear, it basically let you define new type of data (not only having to work with int, char, double, etc). ADT's encapsulate data and different operations for any type of data and it also does not depend of how the data is stored or implemented. They are they "way" to abstract the real world because you could create any type of data.

### Class

A class is a data structure that implements an ADT. It represents the common characteristics in a group of objects (abstraction).

For example, we can think in a class called "car" and create objects that may have different characteristics, like different colors or different names, but they all have something in common, they all have 4 wheels, a motor, a gear mechanism, etc.

<img
    src="images/clssobjc.png"
    alt="class representation"
/>

The image above shows how a <code>Car</code> object can be the template for many other <code>Car</code> instances. A class not only can define a <code>Car</code> object's atributtes (color, number of passengers it can take, etc), but it also can define how it is going to work, or what are going to be its methods (operations). For example, we could create a method <code>accelerate</code> that changes the object's current speed.

### Object

An object is simply an instance of a class, an element of the computer system. It has its singular characteristcs as *Behavior*, *State* and *Identity*.

Example: Lamp

* Behavior - Turn On, Turn Off, getState.
* State - On, Off.
* Identity - Living Room Lamp.

### Attribute

An attribute is basically a class' property. It represents the data.

### Operation

An operation is just specifies which functionality an object supports, but it has no implementation. It is similar to a function prototype as we usually see in C language.

### Method

A method is a implementation of an operation. 

**Note:** We usually don't use the term operation, we refer as methods.

## 2 - Encapsulation

A good habbit to have when programming is to separate your code in modules. One of the modularity principles is the *Data Hiding*, it is useful because it hides the module details from ther modules. So it separates the purpose of your implementation and also retriscts access to other implementation details to any other data structure from the module.

Here in OOP the *Data Hiding* is called *Encapsulation*. To be more clear, it let us hide unecessary details from other classes which are not needed to understand the characteristcs of the class we are working at the moment.

### Access Specifiers

Access specifiers are used for determining or setting the boundary for the availability of class members (data members and member functions) beyond that class.

For example, the class members are grouped into sections, `private` `protected` and `public`. These keywords are called access specifiers which define the accessibility or visibility level of class members.

By default the class members are `private`. So if the visibility labels are missing then by default all the class members are `private`.

In inheritance (we will discuss this later in other topics), it is important to know when a member function in the base class can be used by the objects of the derived class. This is called accessibility and the access specifiers are used to determine this.

* `public` = objects from **any** other class can access
* `private` = access restricted only to objects from the class
* `protected` = access restricted only to objects from the class and its derived classes

`check out Example 1 on "Examples (commented)" section`

### Getters and Setter Methods

Getters and Setters allow you to effectively protect your data. This is a technique used greatly when creating classes. For each variable, a get method will return its value and a set method will set the value.

Check out the **example** below:

```c++
#include <iostream>
using namespace std;

class Employee {
  private:
    int salary; // The salary attribute is private, which have restricted access.

  public:
    void setSalary(int s) {
      salary = s; 
      // The public setSalary() method takes a parameter (s) and 
      // assigns it to the salary attribute (salary = s).
    }
    int getSalary() {
      return salary; 
      // The public getSalary() method returns the value of 
      // the private salary attribute.
    }
};

// Inside main(), we create an object of the Employee class. 
// Now we can use the setSalary() method to set the value of the 
// private attribute to 50000. Then we call the getSalary() 
// method on the object to return the value.

int main() {
  Employee* MrFeather;
  MrFeather.setSalary(50000);
  cout << MrFeather.getSalary();
  return 0;
}
```

### Source File Organization: ".h" and ".cpp" Files

Organization may be something that we could not give so much importance for basic programs like the example above, but when we are making or we are part of a bigger project with hundereds, thousands or even millions of lines of code or classes this is the most important virtue so we can continue developing and sharing this development with other people.

In C++ we organize our files in three main files, the **HEADER** files which have the extension `.h` on their names. so if the name of the file is "example" the header file's name is `example.h`. There's also the **SOURCE** files which have the extension `.cpp`, so the example's source file nasme is `example.cpp`. And finally the code which is going to be the executable program, the `main.cpp`.

**NOTE:** All the .cpp files must be compiled, since they include the header files we don't need to compile the .h files

The same **Example** of the topic above could be separated like this:

**1. Header File**

```c++
#include <iostream>
using namespace std;

class Employee {
  private:
    int salary;

  public:
    void setSalary(int s); // method only declared but not implemented
    int getSalary(); // method only declared but not implemented
};
```

**2. Source File**
```c++
#include "Employee.h" // includes the 'code' of the header

void setSalary(int s) {
      salary = s;   // method implementation
}
int getSalary() {
  return salary;    // method implementation
}
```

**3. Main File**

```c++
#include "Employee.h"
#include <iostream>
using namespace std;

int main() {
  Employee* MrFeather;
  MrFeather.setSalary(50000);
  cout << MrFeather.getSalary();

  return 0;
}
```

### Object Vector

## 3 - Constructors and Destructors

## 4 - Inheritance and Polymorphism

## 5 - Abstract Classes and Multiple Inheritance

## 6 - Error Handling

## 7 - Data Persistence

## 8 - Namespace, Templates and Standard Libraries

## 9 - Reference

The reference to this guide is mostly based on a discipline (PCS3111 - Laboratório de Programação Orientada à Objetos para Engenharia Elétrica) given by the **Computer Engineering and Digital Systems Department (PCS)** from **Escola Politécnica da Universidade de São Paulo** to Electrical Enginerring Students on their second semester. 

The complete material is available, in Portuguese, in this repository.

## 10 - Examples (commented)



1. The Following code shows how a class is defined in C++.

    ```c++
    #include <iostream>

    using namespace std;

    class Lampada {
        public:
            Lampada();
            ~Lampada();

            void ligar();
            void desligar();
            void imprimir();
            
        private:
            bool acesa;
            double potencia;
    };
    ```

    Now let's see how the class' methods were implemented in this case.

    ```c++
    Lampada::Lampada(){
        acesa = false;
        cout << "objeto construido com sucesso" << endl;
    }

    Lampada::~Lampada(){
        cout << "Lampada destruida" << endl;
    }

    void Lampada::ligar() {
        acesa = true;
    }

    void Lampada::desligar() {
        acesa = false;
    }

    void Lampada::imprimir() {
        cout << acesa << endl;
    }

    ```

#### Useful Links

<a href="https://docs.google.com/document/d/136qoVExYsV5zqmuF49-Rm3RgqCdc9mjc4prDhwLXV2U/edit">Plot</a> written to help the workshop given in 12/22/2019.

<a href="http://www.trytoprogram.com/cplusplus-programming/access-specifiers/">OOP reference</a>