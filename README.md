# Clean Code - Smells and Heuristics

## Comments
### C1 Inappropriate Information
Comments should be about the code or project. It shouldn't contains metadata information (git issues, backlog numbers, change history).

Suggestion: Delete or update it.

:-1:
```` java
/* 
 * Change history:
 * Renan Roggia - 8/23/2019 - added behavior X
 * Renan Roggia - 2/19/2019 - fix issue #90
 */
````

### C2 Obsolete Comment
Any comment that does not reflect the actual state of the code.

Suggestion: Delete or update it.

:-1:
````java
private int minuteInSeconds; // Minute in milliseconds
````

### C3 Redundant Comment
When the comment don't add any information.

Suggestion: Delete or update it.

:-1:
````java
private int minuteInSeconds; // Minute in Seconds

/**
 * @param string
 * @return
 */
 public boolean doSomething(String string) {
   //
 }
````

### C4 Poorly Written Comment
The comment is not brief, concise, polite or correctly spelled. 

Suggestion: Update it.

:-1:
````java
rpnChange(0, 2 << 7);   // Bitch Bend sensitivity  <-- typo in jdk

/**
 * This method returns the Nth bit that is set in the bit array. The
 * current position is cached in the following 4 variables and will
 * help speed up a sequence of next() call in an index iterator. This
 * method is a mess, but it is fast and it works, so don't fuck with it.  <-- unnecessary comment in jdk
 */
````
[Typo comment in JDK](http://cr.openjdk.java.net/~afarley/8215217/webrev/src/java.desktop/share/classes/com/sun/media/sound/SoftChannel.java.cdiff.html)

[Unnecessary comment in JDK](http://cr.openjdk.java.net/~afarley/8215217/webrev/src/java.xml/share/classes/com/sun/org/apache/xalan/internal/xsltc/dom/BitArray.java.cdiff.html)

### C5 Commented-Out Code
Any commented code.

Suggestion: Delete it, you can always use the version control system to retrieve it.

:-1:
````java
private String name;
private int age; 
//private String address;  // we might require it in the future
//private String city;
private int numberOfCats;
````

## Environment 
### E1: Build Requires More Than One Step 
Builds should require one command to check out and one command to run.

:+1:
````
git clone https://github.wdf.sap.corp/I840973/code-review.git
[mvn clean install | gradle build] 
````

### E2: Tests Require More Than One Step
Tests should be run with one button click through an IDE, or else with one command. 

:+1:
````
[mvn test | gradle test]
````

## Functions 
### F1 Too Many Arguments 
Ideally, functions shouldn't have arguments, if not possible, one, two at max three. The bigger the argument's number the higher is the consumer's pain to use the function. It's also more difficult to achieve a good test coverage for the function.

Suggestion: Consider refactoring.

:-1:
````java
public boolean doSomething(String arg1, String arg2, String arg3, String arg4, String arg5) {
  //
}
````

### F2 Output Arguments
Avoid using input parameter as output parameters. If your function has to update the state of an object, update its own state.

Suggestion: Consider refactoring.

:-1:
````java
 public void read(MyObject myObject) {
    myObject.setAttribute("changing it muahaha");
 }
````

### F3 Flag Arguments
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

### F4 Dead Function
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

## General 
### G1 Multiple Languages in One Source File
Having multiple languages in the same source file difficults readability.

Suggestion: Split in different source files.

:-1:
````java
public void doSomething(String title) {
    String html = "<!DOCTYPE html>\r\n" + "<html>\r\n" + "<head>\r\n" + "    <title>Something</title>\r\n"
                + "</head>\r\n" + "<body>\r\n" + "    <div>\r\n" + "        <h1>First div title</h1>\r\n"
                + "        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua</p>\r\n"
                + "    </div>\r\n" + "\r\n" + "    <div>\r\n" + "        <h1>Second div title</h1>\r\n"
                + "        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua</p>\r\n"
                + "    </div>\r\n" + "</body>\r\n" + "</html>";

    html = html.replace("Something", title);
    System.out.println(html);
}
````

### G2 Obvious Behavior is Unimplemented
Always implement the obvious expected behavior, otherwise developers will lose confidence in your code.

Suggestion: Implement the obvious behavior, or if not possible you should explain in the documentation why not.

:-1:
````java
public void read(MyObject myObject) {
    write(myObject);
}
````

### G3 Incorrect Behavior at the Boundaries
It's common to find bugs in the boundaries of the system. 

Suggestion: Ensure boundaries are being tested.

:-1:
````java
public void doSomething(String word) {
        switch (word.toUpperCase()){
        case "WORD1":
            System.out.println("do1 and exit");  // <-- didn't test this case statement and forgot break statement. Bug
        case "WORD2":
            System.out.println("do2 and exit");
            break;
        default:
            System.out.println("exit");
        }
    }
````

### G4 Overridden Safeties 
Test and compiler checks are usefull to warn you something might be wrong. Disabling it will only bring you troubles.

Suggestion: fix the test, in case of compiler warning, refactor or only disable it if you are certain the error won't happen and add a comment explaing why.

:-1:
````java
@Ignore
@Test
public void testSomething() {
    //
}

@SuppressWarnings("unchecked")
public <E> E[] doSomething(E... vararg) {
    return vararg;
}

````

### G5 Duplication 
Whenver you find duplicate code, it means you lost a chance for abstraction. Duplicated identical code, repetition of `switch/case` and `if/else` in several methods, same implementation of an algorithm but written differently.

Suggestion: Simplify by adding a layer of abstraction.

:-1:
````java
public String getStringWithBiggerLength(List<String> words) {
    String wordWithBiggerLength = words.get(0);

    for (int i = 1; i < words.size(); i++) {
        if (wordWithBiggerLength.length() < words.get(i).length()) {
            wordWithBiggerLength = words.get(i);
        }
    }
    return wordWithBiggerLength;
}

public boolean isBiggerThanWordWithBiggerLenght(List<String> words, String word) {
    String wordWithBiggerLength = words.get(0);

    for (int i = 1; i < words.size(); i++) {
        if (wordWithBiggerLength.length() < words.get(i).length()) {
            wordWithBiggerLength = words.get(i);
        }
    }
    return wordWithBiggerLength.length() < word.length();
}
````

### G6 Code at Wrong Level of Abstraction 

### G7 Base Classes Depending on Their Derivatives 

### G8 Too Much Information 

### G9 Dead Code

### G10 Vertical Separation 

### G11 Inconsistency 

### G12 Clutter

### G13 Artificial Coupling 

### G14 Feature Envy

### G15 Selector Arguments

### G16 Obscured Intent 

### G17 Misplaced Responsibility 

### G18 Inappropriate Static

### G19 Use Explanatory Variables

### G20 Function Names Should Say What They Do

### G21 Understand the Algorithm

### G22 Make Logical Dependencies Physical

### G23 Prefer Polymorphism to If/Else or Switch/Case

### G24 Follow Standard Conventions

### G25 Replace Magic Numbers with Named Constants 

### G26 Be Precise 

### G27 Structure Over Convention

### G28 Encapsulate Conditionals

### G29 Avoid Negative Conditionals

### G30 Functions Should Do One Thing

### G31 Hidden Temporal Couplings

### G32 Don’t Be Arbitrary

### G33 Encapsulate Boundary Conditions

### G34 Functions Should Descend Only One Level of Abstraction 

### G35 Keep Configurable Data at High Levels

### G36 Avoid Transitive Navigation 

## Names 
* N1: Choose Descriptive Names Choose names that are descriptive and relevant. 
* N2: Choose Names at the Appropriate Level of Abstraction Think of names that are still clear to the user when used in different programs. 
* N3: Use Standard Nomenclature Where Possible Use names that express their task. 
* N4: Unambiguous Names Favor clearness over curtness. A long, expressive name is better than a short, dull one. 
* N5: Use Long Names for Long Scopes A name's length should relate to its scope. 
* N6: Avoid Encodings No not encode names with type or scope information. 
* N7: Names Should Describe Side-Effects Consider the side-effects of your function, and include that in its name. 

### Tests 
* T1: Insufficient Tests Test everything that can possibly break 
* T2: Use a Coverage Tool! Use your IDE as a coverage tool. 
* T3: Don’t Skip Trivial Tests ... 
* T4: An Ignored Test is a Question about an Ambiguity If your test is ignored, the code is brought into question. 
* T5: Test Boundary Conditions The middle is usually covered. Remember the boundaries. 
* T6: Exhaustively Test Near Bugs Bugs are rarely alone. When you find one, look nearby for another. 
* T7: Patterns of Failure Are Revealing Test cases ordered well will reveal patterns of faiure. 
* T8: Test Coverage Patterns Can Be Revealing Similarly, look at the code that is or is not passed in a failure. 
* T9: Tests Should Be Fast Slow tests won't get run.
