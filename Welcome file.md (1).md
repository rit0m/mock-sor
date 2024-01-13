
# JUnit 5, Mockito: A Beginner's Guide

## Table of Contents

1.  Introduction
2.  Setting Up JUnit 5 and Mockito with Maven
3.  Writing Your First JUnit 5 Test
4.  JUnit 5 Annotations
5.  Introduction to Mockito
6.  Mocking with Mockito
7.  The Three Basic Steps in Using Mockito
8.  Understanding and Testing ArrayList Operations - A Step-by-Step Guide
    -   Introduction
    -   Class: `ArraylistTest`
    -   Class: `TestMain`
    -   Importance of Stubbing
    -   Example: Calculator Class
    -   Example: Calculator Test with Stubbing
    -   Conclusion
9.  Introduction to `@Mock` and `@InjectMocks` Annotations
    -   Example: BankService and AccountManager
    -   Explanation
10.  JUnit Best Practices
11.  Mockito Best Practices

## Introduction

This guide will cover the basics of using JUnit 5 and Mockito with Maven, focusing on simple Java classes and collections.

## Setting Up JUnit 5 and Mockito with Maven

Update your `pom.xml` to include the dependencies for JUnit 5 and Mockito:

    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.8.1</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.mockito</groupId>
            <artifactId>mockito-core</artifactId>
            <version>3.12.4</version>
            <scope>test</scope>
        </dependency>
    </dependencies>` 

## Writing Your First JUnit 5 Test

Create a simple Java class `Calculator` and a test class `CalculatorTest`:

    import org.junit.jupiter.api.Test;
    import java.util.ArrayList;
    import static org.junit.jupiter.api.Assertions.assertEquals;
    
	    public class Calculator {
	    
	        public int add(int a, int b) {
	            return a + b;
	        }
	    }
	    
	    public class CalculatorTest {
	    
	        @Test
	        void testAddition() {
	            Calculator calculator = new Calculator();
	            int result = calculator.add(2, 3);
	            assertEquals(5, result);
	        }
	    }
	    
## JUnit 5 Annotations

JUnit 5 annotations remain the same as mentioned earlier:

-   `@Test`: Denotes a test method.
-   `@BeforeEach`: Executed before each test method.
-   `@AfterEach`: Executed after each test method.
-   `@BeforeAll`: Executed once before any test methods.
-   `@AfterAll`: Executed once after all test methods.

## Introduction to Mockito

Mockito is a mocking framework for Java. It allows you to create and use mock objects for testing.

## Mocking with Mockito

Let's create a simple example using Mockito to mock an `ArrayList`:

    import org.junit.jupiter.api.Test;
    import org.mockito.Mockito;
    import java.util.ArrayList;
    
    import static org.junit.jupiter.api.Assertions.assertEquals;
    
    public class ArrayListMockingTest {
    
        @Test
        void testArrayListMocking() {
            // Creating a mock object
            ArrayList<String> mockList = Mockito.mock(ArrayList.class);
    
            // Stubbing the mock object
            Mockito.when(mockList.size()).thenReturn(5);
    
            // Using the mock object
            int size = mockList.size();
    
            // Verifying the interaction
            assertEquals(5, size);
        }
    }
## The Three Basic Steps in Using Mockito

When using Mockito, follow these three basic steps:

### Step 1: Create a Mock Object

Use `Mockito.mock()` to create a mock object for the class or interface you want to mock.

### Step 2: Stubbing

Use `Mockito.when()` to stub/mock method calls on the mock object, specifying the expected behavior.

### Step 3: Verify/Assert

Use assertions and `Mockito.verify()` to ensure that the expected interactions with the mock object occurred.


# Understanding and Testing ArrayList Operations - A Step-by-Step Guide

## Introduction

This documentation aims to provide a clear understanding of ArrayList operations and how to use Mockito for testing. We will analyze the provided classes, identify potential scenarios, and demonstrate testing techniques for new learners.

## Class: `ArraylistTest`

### Code Analysis

    import java.util.ArrayList;
    
    public class ArraylistTest {
    
        public static void main(String[] args) {
            // Creating a real ArrayList
            ArrayList<Integer> arrayList = new ArrayList<>();
            arrayList.add(20000);
            System.out.println(arrayList.get(0));  // Output: 20000
    
            // Creating a mocked ArrayList
            ArrayList<Integer> mockedArrayList = mock(ArrayList.class);
            mockedArrayList.add(1000);
            System.out.println(mockedArrayList.get(0));  // Output: null
        }
    }

### Explanation

-   An actual `ArrayList` (`arrayList`) is created, an integer `20000` is added to it, and then retrieved using `get(0)`.
-   A mocked `ArrayList` (`mockedArrayList`) is created using Mockito's `mock()` method. An integer `1000` is added, but the behavior of `get(0)` is not stubbed.

## Class: `TestMain`

### Code Analysis

    `import java.util.ArrayList;
    
    import static org.mockito.Mockito.*;
    
    public class TestMain {
    
        public static void main(String[] args) {
            // Creating a real ArrayList
            ArrayList<Integer> arrayList = new ArrayList<>();
            arrayList.add(1000);
            System.out.println(arrayList.get(0));  // Output: 1000
    
            // Creating a mocked ArrayList
            ArrayList<Integer> mockList = mock(ArrayList.class);
            // Stubbing the behavior for get(0)
            when(mockList.get(anyInt())).thenReturn(2000);
            // Performing operation
            System.out.println(mockList.get(0));  // Output: 2000
        }
    }

### Explanation

-   An actual `ArrayList` (`arrayList`) is created, an integer `1000` is added to it, and then retrieved using `get(0)`.
-   A mocked `ArrayList` (`mockList`) is created using Mockito's `mock()` method. The behavior for `get(0)` is stubbed to return `2000`, and then `get(0)` is invoked.

## Importance of Stubbing

### Why Stubbing is Important

Stubbing in testing serves two crucial purposes:

1.  **Controlled Behavior:** Stubbing allows you to control the behavior of methods in your mocked objects. This is essential for isolating the behavior you want to test and ensuring that the test environment is predictable.
    
2.  **Isolation:** It isolates the unit of code being tested, making the test focus on specific functionality without worrying about the behavior of other components. Stubbing helps create a controlled environment for testing.
    

### Consequences of Not Using Stubbing

When stubbing is neglected, several issues may arise:

1.  **Unpredictable Results:** Without stubbing, method calls on mock objects may produce unpredictable results, leading to inconsistent and unreliable test outcomes.
    
2.  **Incorrect Verifications:** In the absence of stubbing, the test may pass even if the actual behavior of the method does not match the expected behavior. This can lead to incorrect verifications in your tests.
    
3.  **Limited Testing Scope:** Without stubbing, it becomes challenging to focus tests on specific scenarios or edge cases. The lack of control over method behaviors limits the effectiveness of your tests.


let's simplify the explanation with an example that demonstrates the importance of stubbing in testing scenarios.

Consider a simple class `Calculator` with a method `divide`:

    `public class Calculator {
        public double divide(double dividend, double divisor) {
            if (divisor == 0) {
                throw new IllegalArgumentException("Cannot divide by zero");
            }
            return dividend / divisor;
        }
    }` 

Now, let's write a test for this class using JUnit and Mockito without proper stubbing:

    `import org.junit.jupiter.api.Test;
    import org.mockito.Mockito;
    
    import static org.junit.jupiter.api.Assertions.assertThrows;
    
    public class CalculatorTest {
    
        @Test
        void testDivideWithoutStubbing() {
            Calculator mockCalculator = Mockito.mock(Calculator.class);
    
            // Without stubbing, the real method is called
            assertThrows(IllegalArgumentException.class, () -> mockCalculator.divide(10.0, 0.0));
        }
    } 

In this example, we're testing the `Calculator` class, specifically the `divide` method. We create a mock of the `Calculator` class using Mockito.

Now, let's analyze the issues with this test:

1.  **Real Method Execution:** Without stubbing, when we call `mockCalculator.divide(10.0, 0.0)`, the real `divide` method of the `Calculator` class is executed. This can lead to unexpected behavior, and in this case, it throws an `IllegalArgumentException` as intended.
    
2.  **Limited Control:** The test lacks control over the behavior of the `divide` method. We want to focus on the scenario where division by zero occurs, but without stubbing, the real method execution takes place, making it harder to isolate and test specific cases.
    

Now, let's modify the test to include proper stubbing:

    `import org.junit.jupiter.api.Test;
    import org.mockito.Mockito;
    
    import static org.junit.jupiter.api.Assertions.assertThrows;
    import static org.mockito.Mockito.when;
    
    public class CalculatorTest {
    
        @Test
        void testDivideWithStubbing() {
            Calculator mockCalculator = Mockito.mock(Calculator.class);
    
            // Stubbing the behavior for divide method
            when(mockCalculator.divide(10.0, 0.0)).thenThrow(new IllegalArgumentException("Cannot divide by zero"));
    
            // With stubbing, the real method is not executed
            assertThrows(IllegalArgumentException.class, () -> mockCalculator.divide(10.0, 0.0));
        }
    }` 

Now, with proper stubbing, we use `when(mockCalculator.divide(10.0, 0.0)).thenThrow(...)` to control the behavior of the `divide` method. This allows us to isolate the scenario where division by zero occurs, providing more control and making the test more focused and reliable.

In conclusion, stubbing is crucial in testing to gain control over the behavior of methods in mocked objects. It helps create a controlled environment for testing specific scenarios, ensuring more accurate and effective tests.


### Introduction to `@Mock` and `@InjectMocks` Annotations

In Mockito, `@Mock` is used to create a mock object for a class or interface, and `@InjectMocks` is used to inject mock instances into the tested object.

### Example: BankService and AccountManager

Consider two classes: `BankService` and `AccountManager`.

#### BankService.java


    import org.springframework.beans.factory.annotation.Autowired;
    
    @Data
    public class BankService {
    
        @Autowired
        private AccountManager accountManager;
    
        public boolean transferMoney(String fromAccount, String toAccount, double amount) {
            double balance = accountManager.getAccountBalance(fromAccount);
            if (balance >= amount) {
                accountManager.withdraw(fromAccount, amount);
                accountManager.deposit(toAccount, amount);
                return true;
            } else {
                return false;
            }
        }
    }

#### AccountManager.java

    public class AccountManager {
    
        public double getAccountBalance(String accountNumber) {
            // Fetch account balance logic
            // Assume fetching from a database or external service
            return 5000.0;
        }
    
        public void withdraw(String accountNumber, double amount) {
            // Withdraw money logic
        }
    
        public void deposit(String accountNumber, double amount) {
            // Deposit money logic
        }
    }

Now, let's write a test class using JUnit, Mockito, and the `@Mock` and `@InjectMocks` annotations.

#### BankServiceTest.java

    import org.junit.jupiter.api.BeforeEach;
    import org.junit.jupiter.api.Test;
    import org.mockito.InjectMocks;
    import org.mockito.Mock;
    import org.mockito.MockitoAnnotations;
    
    import static org.junit.jupiter.api.Assertions.assertFalse;
    import static org.junit.jupiter.api.Assertions.assertTrue;
    import static org.mockito.Mockito.when;
    
    public class BankServiceTest {
    
        @Mock
        private AccountManager mockAccountManager;
    
        @InjectMocks
        private BankService bankService;
    
        @BeforeEach
        void setUp() {
            MockitoAnnotations.openMocks(this);
        }
    
        @Test
        void testTransferMoneySufficientBalance() {
            // Stubbing behavior for AccountManager
            when(mockAccountManager.getAccountBalance("123")).thenReturn(10000.0);
    
            // Testing BankService with mocked AccountManager
            boolean result = bankService.transferMoney("123", "456", 500.0);
    
            assertTrue(result);
        }
    
        @Test
        void testTransferMoneyInsufficientBalance() {
            // Stubbing behavior for AccountManager
            when(mockAccountManager.getAccountBalance("789")).thenReturn(200.0);
    
            // Testing BankService with mocked AccountManager
            boolean result = bankService.transferMoney("789", "987", 1000.0);
    
            assertFalse(result);
        }
    }


#### Explanation

-   `@Mock`: The `@Mock` annotation is used to create a mock instance of the `AccountManager` class. It tells Mockito to create a mock for the specified class or interface.
    
-   `@InjectMocks`: The `@InjectMocks` annotation is used to inject the mock instances into the tested object, in this case, the `BankService` class.
    
-   `MockitoAnnotations.openMocks(this)`: This line initializes annotated fields (`@Mock` and `@InjectMocks`) in the test class. It is typically done in the `@BeforeEach` method.
    
-   `when(mockAccountManager.getAccountBalance("123")).thenReturn(10000.0)`: This line stubs the behavior of the `getAccountBalance` method for the mock `AccountManager` instance. It specifies that when the method is called with the account number "123," it should return a balance of 10000.0.
    
-   The test methods (`testTransferMoneySufficientBalance` and `testTransferMoneyInsufficientBalance`) then demonstrate testing different scenarios of money transfer using the `BankService` class with the mocked `AccountManager`.
    

In conclusion, the `@Mock` and `@InjectMocks` annotations in Mockito facilitate the creation of mock objects and injection of those mocks into the tested objects, providing a cleaner and more concise way to set up and test interactions between components in your application.


**@Mock:**

-   Think of it as creating imitation parts for a car that you can use during testing.
-   Example:

>      @Mock
>         private Engine mockEngine;

    
-   Here, `mockEngine` is a pretend or fake engine that you'll use instead of a real one for testing.

**@InjectMocks:**

-   Think of it as putting those imitation parts into the actual car you want to test.
-   Example:
    

>     @InjectMocks   
>     private Car carUnderTest;

    
-   Here, `carUnderTest` is the real car you want to test, and it gets its fake or mock engine automatically inserted.

**Difference:**

-   `@Mock` helps you make pretend car parts (like a fake engine).
-   `@InjectMocks` helps you place those pretend parts into a real car to see how it performs.

**New Analogy - Building a Car:**

-   `@Mock` is like creating a cardboard engine to test how the car reacts without a real one.
-   `@InjectMocks` is like putting that cardboard engine into a real car frame to see how well it drives with the fake engine.

In summary, `@Mock` lets you make fake parts for testing, and `@InjectMocks` lets you use those fake parts in the real thing you want to test, much like testing a car with a fake engine before putting in the real one.

## JUnit Best Practices:

-   **Organize Test Cases:**
    
    -   Group test cases logically into test classes. Use meaningful class and method names for better clarity.
-   **Single Responsibility:**
    
    -   Aim for each test case to focus on a single behavior or scenario. Avoid testing too many things in a single test case.
-   **Use Annotations Wisely:**
    
    -   Utilize JUnit annotations such as `@Before`, `@After`, `@BeforeEach`, and `@AfterEach` for setup and cleanup tasks.
-   **Assertions:**
    
    -   Use descriptive assertions to clearly convey what is being tested. Prefer using JUnit's built-in assertions or assert libraries like AssertJ.
-   **Parameterized Tests:**
    
    -   For multiple input scenarios, consider using parameterized tests (`@ParameterizedTest`) to avoid duplicating similar test logic.
-   **Timeouts:**
    
    -   Set timeouts (`@Test(timeout)`) for tests that should complete within a specified time to avoid prolonged test execution.
-   **Ignore Tests Sparingly:**
    
    -   Avoid using `@Ignore` unless absolutely necessary. It's better to fix or remove the test rather than ignoring it.

-   **Test Coverage:**
    
    -   Aim for good test coverage, testing both positive and negative scenarios, as well as edge cases.
    - 
**Avoid Reflection API for Testing Private Methods:**

-   **Prefer Public Interface:**
    
    -   Test through the public methods to ensure stability and resist changes during refactoring.
## Mockito Best Practices:

-   **Mock Only What You Own:**
    
    -   Mock objects that you have control over. Avoid mocking external dependencies unless necessary.
-   **Clear Test Method Names:**
    
    -   Make test method names descriptive, specifying what behavior is being tested with mocks.
-   **Use @Mock Annotation:**
    
    -   Annotate mock objects with `@Mock` for clarity. It's especially helpful in larger test classes.
-   **Annotations Initialization:**
    
    -   Initialize annotations like `@Mock` using `MockitoAnnotations.initMocks(this)` in `@Before` or `@BeforeEach` methods.
-   **Verify Interactions:**
    
    -   Use `verify` to check that a method on a mock has been called with specific arguments.
-   **Stubbing Methods:**
    
    -   Stub only the necessary methods. Avoid unnecessary stubbing, as it can lead to brittle tests.
-   **Reset Mocks Sparingly:**
    
    -   Avoid using `Mockito.reset(mock)` unless necessary. It's usually better to create new mocks for each test.
-   **Spy with Caution:**
    
    -   Use spies (`@Spy`) carefully. Prefer mocks over spies, and be cautious about partial mocking.
-   **Avoid Excessive Mocking:**
    
    -   Strive for a balance between mocking and real objects. Excessive mocking can lead to tests that are too isolated from real-world scenarios.
-   **Clean Verification:**
    
    -   Use `verifyNoMoreInteractions` after the actual verifications to ensure that no unexpected interactions occurred.




