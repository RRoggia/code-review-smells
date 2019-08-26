# Functions 
## F1 Too Many Arguments 
Ideally, functions shouldn't have arguments, if not possible, one, two at max three. The bigger the argument's number the higher is the consumer's pain to use the function. It's also more difficult to achieve a good test coverage for the function.

Suggestion: Consider refactoring.

:-1:
````java
public boolean doSomething(String arg1, String arg2, String arg3, String arg4, String arg5) {
  //
}
````

## F2 Output Arguments
Avoid using input parameter as output parameters. If your function has to update the state of an object, update its own state.

Suggestion: Consider refactoring.

:-1:
````java
 public void read(MyObject myObject) {
    myObject.setAttribute("changing it muahaha");
 }
````

## F3 Flag Arguments
`boolean` arguments used to create two branches of code are explicitly showing that the code does has more than one responsibility.

Suggestion: Consider refactoring.

:-1:
````java
public boolean doAorB(boolean bool) {
    if (bool) {
        //do A
    } else {
        //do B
    }
}
````

## F4 Dead Function
Functions that are not used and are not part of your public API are dead functions.

Suggestion: Delete these functions

:-1:
````java
public class Class {

    public void doSomething() {
        // ..
    }

    private void dontDoSomething() {
        // unreacheable by client code and never used. Delete it.
    }
}
````
