# Lab-8_202001156
# Name - Ayush Khamar
# ID - 202001156



## Creating Java Package and Boa Class

The Boa class implementation is housed in a package called Lab08. The corresponding.java code is as follows:



```java
package Lab08;

/* represents a Boa Constrictor */
public class Boa {
	private String name;
	private int length; // the length of the boa, in feet
	private String favoriteFood;

	public Boa (String name, int length, String favoriteFood) {
		this.name = name;
		this.length = length;
		this.favoriteFood = favoriteFood;
	}
	public boolean isHealthy() {
		/* returns true if this boa constrictor is healthy */
		return this.favoriteFood.equals("granola bars");
	}
	public boolean fitsInCage(int cageLength) {
		/* returns true if the length of this boa constrictor is
	 	  less than the given cage length */
		return this.length < cageLength;
	}
}
```

## Creating a JUnit Test Class in Eclipse

JUnit test cases can be added to any.java file by right-clicking the file, selecting new, and then selecting JUnit Test Case. We make the BoaTest.java test case file for the Boa.java file.

The setUp() function is defined after the test case file has been set up.



```java
package Lab08;

import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.AfterAll;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

class BoaTest {
	private Boa jen, ken;

	@BeforeEach
	void setUp() throws Exception {
		jen = new Boa("Jennifer", 2, "grapes");
		ken = new Boa("Kenneth", 3, "granola bars");
	}
	@AfterEach
	void tearDown() throws Exception {
	}
	@Test
	final void testIsHealthy() {
		fail("Not yet implemented"); // TODO
	}
	@Test
	final void testFitsInCage() {
		fail("Not yet implemented"); // TODO
	}
}
```

> Note that the methods _testIsHealthy()_ and _testFitsInCage()_ will contain code to test the _Boa_ class methods. These functions along with _tearDown()_ are yet to be implemented.

## Testing _Boa_ class methods

### _isHealthy()_ method

It's crucial to remember that the _isHealthy()_ function has no parameters. As a result, the method can only be called on the _Boa_ objects _"jen" and _"ken" in test situations.  
The following are the test cases listed in the _testIsHealthy()_ test function:


```java
final void testIsHealthy() {
    assertFalse(jen.isHealthy());
    assertTrue(ken.isHealthy());
}
```

> The cases are defined so because _jen_ does not have favoriteFood as _"granola bar"_ which is necessary for boa object to be healthy while _ken_ has favoriteFood as _"granola bar"_.

### _FitsInCage()_ method

There are numerous test cases that could be possible because the _FitsInCage()_ function accepts an integer parameter as input.  
It is preferable to call methods from both instances to guarantee that the function definition is independent of the instance even if _jen_ and _ken_ will both be executing the same function definition for the _FitsInCage(cage_length>) function call.


The test-cases defined can thus go as follows:

```java
final void testFitsInCage() {
    // invalid length input
    assertFalse(jen.fitsInCage(-1));
    assertFalse(jen.fitsInCage(-3));

    // cage larger than boa
    assertTrue(jen.fitsInCage(10));
    assertTrue(ken.fitsInCage(6));

    // cage smaller than boa
    assertFalse(jen.fitsInCage(0));
    assertFalse(ken.fitsInCage(1));

    // cage length equal to boa
    assertTrue(jen.fitsInCage(2));
    assertTrue(jen.fitsInCage(3));
}
```

> Here, the test cases will be roughly separated into two partitions, which correspond to the boundary conditions of cage length equal to _Boa_ and lengths less than _Boa_, more than _Boa_, and equal to _Boa_.

> The first two test cases also take into account negative lengths, which are associated with erroneous input for lengths and must always return false.


## Running the Test Cases

To run the test cases, we simply right-click on the file(_BoaTest.java_ here), click on _Coverage As_, and then _1 JUnit Test_.

![image](https://user-images.githubusercontent.com/123557378/233040908-c781624e-c3ed-4503-adea-7be1aa2272ea.png)

> Here, the last two test cases fail indicating an error in the code. The error occurs in the _isHealthy()_ function which is defined as follows:

```java
public boolean fitsInCage(int cageLength) {
    return this.length < cageLength;
}
```

To correct this error, the actual definition of the function should be like as shown below to account for the fact that the boa can fit in a cage equal to its length (even if not comfortably).

```java
public boolean fitsInCage(int cageLength) {
    return this.length <= cageLength;
}
```

With the modified code, we can see that all the test-case successfully pass now

![image](https://user-images.githubusercontent.com/123557378/233041915-e4c42123-32f8-4f2e-a7a1-af1651daf218.png)

## Adding new Method

we add a new method _lengthInches()_ to return the length of the Boa in inches.

```java
public int lengthInches(){
    return this.length * 12;
}
``
```

The new test cases defined for the same are as follows:

```java
final void testLengthInches() {
    assertEquals(jen.lengthInches(), 24);
    assertEquals(ken.lengthInches(), 36);
}
```
The test case pass successfully as shown below

![image](https://user-images.githubusercontent.com/123557378/233043302-50ee4e3f-c753-4dd8-9e0b-73fb6c51ae58.png)
