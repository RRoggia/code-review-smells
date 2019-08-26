# Environment 
## E1: Build Requires More Than One Step 
Builds should require one command to check out and one command to run.

:+1:
````
git clone https://github.wdf.sap.corp/I840973/code-review.git
[mvn clean install | gradle build] 
````

## E2: Tests Require More Than One Step
Tests should be run with one button click through an IDE, or else with one command. 

:+1:
````
[mvn test | gradle test]
````
