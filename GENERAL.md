# General 
## G1 Multiple Languages in One Source File
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

## G2 Obvious Behavior is Unimplemented
Always implement the obvious expected behavior, otherwise developers will lose confidence in your code.

Suggestion: Implement the obvious behavior, or if not possible you should explain in the documentation why not.

:-1:
````java
public void read(MyObject myObject) {
    write(myObject);
}
````

## G3 Incorrect Behavior at the Boundaries
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

## G4 Overridden Safeties 
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

## G5 Duplication 
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

## G6 Code at Wrong Level of Abstraction 
Keep consistent the level of abstraction you are using in your code, component, module, system ...

Suggestion: Refactor to achieve the same abstraction level of the rest of your code...

:-1:
````java
public Document persist(Document document) {
    validate(document);

    if (alreadyExists(document)) {
        return document;
     }

    Connection conn = null;
    Properties connectionProps = new Properties();
    connectionProps.put("user", this.userName);
    connectionProps.put("password", this.password);

    conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/", connectionProps);
        
    Statement stmt = conn.createStatement();
        
    stmt.executeUpdate("insert into ...");
}
````

## G7 Base Classes Depending on Their Derivatives 
Breaking the logic of a base class in deratives, means you are adding an abstraction level in your code. Therefore, if the base class is dependant of the derivative class' internal behaviors, there might be a problem.

Suggestion: Refactor the base class to not depend on the derivative internal behavior.

:-1:
````java
class ControllerClazz{
    
    public void doSomething(){
        ServiceClazz serviceClazz = new ServiceClazz();
        List<String> namesSorted = serviceClazz.getNamesSorted();
        
        for(String name: namesSorted) {
            //
        }
            
        new ServiceClazz2().doSomething();
    }
    
}

class ServiceClazz{
    public void doSomething() {
        getNamesSorted();
        //
    }
    
    public List<String> getNamesSorted(){
        //
    }
}

class ServiceClazz2{
    public void doSomething() {
        
    }
}
````

## G8 Too Much Information 
A well defined API has just enought information to do a lot with litle information. The less information you expose the less coupling with client classes.

Suggestion: Reduce the information you are exposing.

:-1:
````java
public class Something {
    public String somethingInternal;
    public static final String INTERNAL_ERROR = "INTERNAL ERROR";
    
    public void doSomething() {
        //
    }
    
    public void doLessThanSomething() {
        //
    }
    
    public void doLessThanLessSomething() {
        //
    }
    
    public String getSomethingInternal() {
        return somethingInternal;
    }
}
````


## G9 Dead Code
Any code that is unreacheable. Either because it got old, or because it's a conditional that not happen.

Suggestion: Remove it.

:-1:
````java
public void doSomething() throws IllegalArgumentException {
    // never throws IllegalArgumentException
}

public void doSomething(String name) {
    Objects.requireNonNull(name);

    if (name == null) {
        throw new NullPointerException("Null pointer");
    }

    System.out.println(name);
}
````

## G10 Vertical Separation 
When a variable or function is declared far away from its usage.

Suggestion: Declare variables before its use, declare functions below its invocation.

:-1:
````java
public void doSomething() {
    String name;
    int age;
    String city;
        
    doAnotherthing();
    processWhatever();
    //...
        
    System.out.println(name);
    System.out.println(age);
    System.out.println(city);
}
````

## G11 Inconsistency 
When decided over a convetion, apply it consistently in other similar situation to avoid surprises and improve readbility.

Suggestion: Refactor the code to achieve the convention.

:-1:
````java
public void doSomething(HttpServletRequest request) {
//
}
    
public void doAnotherThing(HttpServletRequest servlet) {
//
}
    
public void doAThirdThing(HttpServletRequest request) {
//        
}
````

## G12 Clutter
Methods, attributes and variables that are not used, comments that don't add anything.

Suggestion: Remove the clutter from your code.

:-1:
````java
public class Class {
    private void dontDoSomething() {
        // unreacheable by client code and never used locally.
    }
}
````

## G13 Artificial Coupling 
A generic variable, constant, function or enum is placed within a specific class.

Suggestion: Decouple the generic component from the specific component.

:-1:
````java
public class Clazz {
    public static enum Country {
        BR, AR, US, GE;
    }
}

public class ClientCode {
    public static void main(String[] args) {
        System.out.println(Clazz.Country.AR);
    }
}
````

## G14 Feature Envy
When a method uses getters and setters from other classes to manipulate this object, the method is envying the feature of the object.

Suggestion: Move the the method that is envying the feature to the object.

:-1:
````java
public class HourlyPayCalculator {
    public Money calculateWeeklyPay(HourlyEmployee e) {
        int tenthRate = e.getTenthRate().getPennies();
        int tenthsWorked = e.getTenthsWorked();
        int straightTime = Math.min(400, tenthsWorked);
        int overTime = Math.max(0, tenthsWorked - straightTime);
        int straightPay = straightTime * tenthRate;
        int overtimePay = (int) Math.round(overTime * tenthRate * 1.5);
        return new Money(straightPay + overtimePay);
    }
}
````

## G15 Selector Arguments
Selector arguments are a lazy to not split a big function into several smaller functions.

Suggestion: Break function into smaller functions.

:-1:
````java
public int calculateWeeklyPay(boolean overtime) {
    int tenthRate = getTenthRate();
    int tenthsWorked = getTenthsWorked();
    int straightTime = Math.min(400, tenthsWorked);
    int overTime = Math.max(0, tenthsWorked - straightTime);
    int straightPay = straightTime * tenthRate;
    double overtimeRate = overtime ? 1.5 : 1.0 * tenthRate;
    int overtimePay = (int) Math.round(overTime * overtimeRate);
    return straightPay + overtimePay;
}
````

## G16 Obscured Intent 
The code must be clear and expressive. Magic numbers, hungarian notation and continuous expressions make harder to read the code.

Suggestion: Refactor to remove the above mentioned smells.

:-1:
````java
public int m_otCalc() {
    return iThsWkd * iThsRte + (int) Math.round(0.5* iThsRte * Math.max(0, iThsWkd - 400));
}
````

## G17 Misplaced Responsibility 
The code is breaking the principle of least surprise. It's not placed in the right class, module or scope.

Suggestion: Change the code to a place where the reader would expect.

:-1:
````java
public class Salary {
    public static final double PI = 3.14159265358979323846;

    public double getSalary() {
        return PI * 1000;
    }
}
````

## G18 Inappropriate Static
A function should be static if it's not dependent on instances and takes all its dependencies from the parameters. It will be innapropriate static if the function fulfills the items above but could benefit from polimorphism.

Suggestion: Change it to an instance member.

:-1:
````java

public class HourlyPayCalculator {
    public static int calculatePay(Employee e, double overtimeRate) {
        //
    }
}

public class OvertimeHourlyPayCalculator {
    public static int calculatePay(Employee e, double overtimeRate) {
        //
    }
}

public class StraightHourlyPayCalculator {
    public static int calculatePay(Employee e, double overtimeRate) {
        //
    }
}
````

## G19 Use Explanatory Variables
The code readability could improve by adding intermediary variables with descritive names.

Suggestion: Add intermediary variables with descritive names.

:+1:
````java
Matcher match = headerPattern.matcher(line);
if (match.find()) {
    String key = match.group(1);
    String value = match.group(2);
    headers.put(key.toLowerCase(), value);
}
````

## G20 Function Names Should Say What They Do
Function name is misleading or is ambiguous.

Suggestion: Rename the function name to better describe it.

:-1:
````java
Date newDate = date.add(5);
````

## G21 Understand the Algorithm
Making the algorith work is not enough, you should comprehend it. Not comprehending it leads to messy code.

Suggestion: Refactor the code to make the algorithm more clear and easier to comprehend.

## G22 Make Logical Dependencies Physical
One should not assume behaviors of a module you are dependent.

Suggestion: Refactor to remove the assumption of your code.

:-1:
````java
public void getDocumentsAndPrintSortedByName() {
    List<Document> documents = databaseConnection.getDocuments();

    for (Document document: documents) {
        System.out.println(document);
    }
}
````

## G23 Prefer Polymorphism to If/Else or Switch/Case
Using `if/else` or `switch/case` statements difficults the addition of new classes without changing existing functions.

Suggestion: Unless is more likely to have new functions than new classes. Refactor the code to use polymorphism.

:-1:
````java
public double area(Object shape) {
    if (shape instanceof Square) {
        Square s = (Square) shape;
        return s.getSide() * s.getSide();
    } else if(shape instanceof Circle) {
        Circle c = (Circle) shape;
        return Math.PI * c.getRadius() * c.getRadius();
    }
}
````

## G24 Follow Standard Conventions
Code not following the standard convetions

Suggestion: Apply the standard conventions

:-1:
````java
public void DO_SOMETHING()
{
    if (true) {
        System.out.println("something");
    }
}
    
public void AnOtHeRtHiNg() {
    if(!false)
        System.out.println("another thing");
}
````

## G25 Replace Magic Numbers with Named Constants 
Any token that posses a value that is not self-explanatory.

Suggestion:Move the value to a constant variable.

:-1:
````java
public double calculateSalary(int overtime) {
    return (8 * 22 + overtime) * 22.5;
}
````

## G26 Be Precise 
Be precise with the decision you are taking in your code. Innacuracy code leads to ambiguity and messy code.

Suggestion: Update or remove inprecission.

:-1:
````java
// using double for amounts
public double payDebt(double amount) {
    debt = debt - amount;
}

// not handling null cases
public void doSomething() {
    getStringOrReturnNull().concat("never gonna give it up");
}
    
public String getStringOrReturnNull() {
    return null;
}
````

## G27 Structure Over Convention
Project decision should be based on structure over conventions.

Suggestions: Refactor the code to use polymorphism.

:-1:
````java
public double area(Object shape) {
    if (shape instanceof Square) {
        Square s = (Square) shape;
        return s.getSide() * s.getSide();
    } else if(shape instanceof Circle) {
        Circle c = (Circle) shape;
        return Math.PI * c.getRadius() * c.getRadius();
    }
}
````

## G28 Encapsulate Conditionals
Complex boolean expressions don't express motivation and are hard to read.

Suggestions: Extract boolean expression to variable with descriptive name.

:-1:
````java
public void doSomething() {
        if (((age > 18 && age < 50) || Date.from(Instant.now()).after(birthday) && city != "Chicago")
                || ((age > 18) && country != "Brazil")) {
        System.out.println("Allowed");
    }
}
````
## G29 Avoid Negative Conditionals
Negative boolean expressions are harder to read than positive.

Suggestion: Change it to be a poisitive boolean expression.

:-1:
````java
if(!buffer.shouldNotCompact())
````
## G30 Functions Should Do One Thing

## G31 Hidden Temporal Couplings

## G32 Don’t Be Arbitrary

## G33 Encapsulate Boundary Conditions

## G34 Functions Should Descend Only One Level of Abstraction 

## G35 Keep Configurable Data at High Levels

## G36 Avoid Transitive Navigation 
