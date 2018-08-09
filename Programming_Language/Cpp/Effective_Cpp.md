# Introduction
## Introduction to some basic structures
#### Constructor should be declared **explicit**, to be prevent to perform implicit type conversations
    class B{
        public:
        explicit B(int x=0, bool b=true); // explicit declarations
    }

    void doSomething(B bObject);

    doSomething(28); //Error! no implicit constructor
    doSomething(B(28)); //fine

#### Copy constructor and copy assignment operator
    class B{
        public:
        B(const B& rhs);            //copy constructor
        B& operator=(const B& rhs); //copy assignment operator
    }
    B b1;
    B b2(b1);   //invoke copy constructor
    b2=b1;      //invoke copy assignment operator
    B b3=b2;    //invoke copy constructor!!!

#### function objects:
objects that act like functions(like iterator)

#### Abbreviation
1. *ctor*: constructor, *dtor*: destructor
2. *ptr*: pointer

### Name conventions
1. `lhs`=left hand side, `rhs`=right hand side
2. `pt`=pointer to class T
3. `rt`=reference to object T

# Accustoming yourself to c++
## Item 1: View C++ as a federation of languages
Page 12
