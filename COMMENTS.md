# Comments
## C1 Inappropriate Information
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

## C2 Obsolete Comment
Any comment that does not reflect the actual state of the code.

Suggestion: Delete or update it.

:-1:
````java
private int minuteInSeconds; // Minute in milliseconds
````

## C3 Redundant Comment
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

## C4 Poorly Written Comment
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

## C5 Commented-Out Code
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
