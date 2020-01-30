# Clean Code - Smells and Heuristics

### [Comments](./COMMENTS.md)
* C1 Inappropriate Information
* C2 Obsolete Comment
* C3 Redundant Comment
* C4 Poorly Written Comment 
* C5 Commented-Out Code

### [Environment](./ENVIRONMENT.md)
* E1 Build Requires More Than One Step
* E2 Tests Require More Than One Step

### [Functions](./FUNCTIONS.md)
* F1 Too Many Arguments
* F2 Output Arguments
* F3 Flag Arguments
* F4 Dead Function

### [General](./GENERAL.md)
* G1 Multiple Languages in One Source File
* G2 Obvious Behavior is Unimplemented
* G3 Incorrect Behavior at the Boundaries
* G4 Overridden Safeties 
* G5 Duplication 
* G6 Code at Wrong Level of Abstraction 
* G7 Base Classes Depending on Their Derivatives 
* G8 Too Much Information 
* G9 Dead Code
* G10 Vertical Separation 
* G11 Inconsistency 
* G12 Clutter
* G13 Artificial Coupling 
* G14 Feature Envy
* G15 Selector Arguments
* G16 Obscured Intent 
* G17 Misplaced Responsibility 
* G18 Inappropriate Static
* G19 Use Explanatory Variables
* G20 Function Names Should Say What They Do
* G21 Understand the Algorithm
* G22 Make Logical Dependencies Physical
* G23 Prefer Polymorphism to If/Else or Switch/Case
* G24 Follow Standard Conventions
* G25 Replace Magic Numbers with Named Constants 
* G26 Be Precise 
* G27 Structure Over Convention
* G28 Encapsulate Conditionals
* G29 Avoid Negative Conditionals
* G30 Functions Should Do One Thing
* G31 Hidden Temporal Couplings
* G32 Don’t Be Arbitrary
* G33 Encapsulate Boundary Conditions
* G34 Functions Should Descend Only One Level of Abstraction 
* G35 Keep Configurable Data at High Levels
* G36 Avoid Transitive Navigation 

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
