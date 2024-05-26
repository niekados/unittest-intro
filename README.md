# Unittest

## The unittest library

This testing framework  is called Unittest.
“Batteries-included” simply means that it comes with everything needed for full usability as standard.
Let's go over what we expect the  function we are going to build should do.
We are going to write a function  that accepts a list of numbers  
and returns true if the list contains  an even number of even numbers. 
It should also raise a TypeError if anything  other than a list is passed into the function.
So let’s pause for a moment and  think about what we should test for?
And this is something you should always  do, even if you are not writing tests.

Our function should raise a TypeError with an error message if a list isn't passed in as an argument.
It should return False when numbers is empty, the numbers of even is odd.
and when the number of evens is zero.
We'd expect it to return True if the numbers of evens is even, however.

So with this list of ideas for tests, I think we  are ready to get started setting up our files.
- I will create two files, one named `evens.py` [name for even numbers] and this is where we will build our function.
And another file which we will name  `test_evens.py`, where we will write our tests.

---
Unittest requires that our test  filename starts with the word ‘`test`’,  
followed by an underscore and a  descriptive name of what we’re testing.

---

- Next, we need to import the Unittest  module into our test_evens.py file.
To do this, we simply type `import Unittest`.  
As mentioned before, Unittest is part of Python’s  standard library, so we don’t need to install it.
- We are now ready to create a test case and we'll do so by creating a class named TestEvens.
To make use of Unittest’s functionality,  
our class needs to inherit  from the `unittest.TestCase` class.
- I'll also add a pass statement and `unittest.main()`. So we can run the file without specifying the unit test module.

And when we run the code using the command `python3 test_evens.py` everything works fine, and we are  
shown in the output that 0 tests were run, which  is fine as we have not created any tests yet. 

You might be wondering what the pass statement does?  Let's comment it out and run the code again.
You will see you get an error. Python is expecting  an indented block after the use of a colon,  
so when you have no code using the pass statement  is valid and allows your code to run error free.

- Let’s move over to our other file and  declare our function. I will name it  
`even_number_of_evens` and give it a parameter  named `numbers` and have it return None.
Underneath it, inside a print method, I will call it and pass it the value five.

```python
def even_number_of_evens(numbers):
    """
    Should Raise a TypeError if a list in not passed into the function
    error message: "A list was not passed into the function"
    if the list is empty it will return False
    if the number of even numbers is odd - return False
    if the numner of even numbers is even - return True
    """
    return None

print(even_number_of_evens(5))

```

When I run this code, I see that our function works and returns None.
I am also going to add our list of test  ideas to our function as a doc string,  
so we can refer to that if we need a  reminder of what we could be testing for.

I want to show a couple of more points  before we start building up our function  
using unit testing, so I will do a  basic test to show how they work.

- First, we need to import our function into our test file.
Now we can write a test to check  everything works and our setup is correct.
So let's create a basic test that tests  whether if our function returns True.   
- It will be a method and needs to start with the word ‘test’.  If we don’t start the method name with the word test,
it will be ignored and won't run, when we run the test file.
And as we are in a class we need to pass in the self keyword.
In here, we can create either a  single assert or many asserts,  
for now we will just create one  just to show you how things work.
So I’ll assertTrue that calling  the function even_number_of_evens  
with an empty list returns True. 

```python
import unittest
from evens import even_number_of_evens

class TestEvens(unittest.TestCase):
    
    def test_function_returns_True(self):
        self.assertTrue(even_number_of_evens([]))


unittest.main()
```

If I run the test, we can see from the output  our test failed and the reason it failed. 
It states an AssertionError None is not True. This makes sense as our  
function is set to return None, it also tells us  the line number and points to the test that fails,  
which makes it handy to figure  out which test is failing.

So let’s make this test pass. Going back  to our function I will change None to True  
and now when we run the test it passes. It shows a period to represent the test  
and states how many tests were run  and OK.
But what is the “True” doing there?
That’s from our function call in our file that contains the function.   
When the test was run this function call was also run.
Let’s prevent that from happening by making  the following change.

---
**NOTE**

So what is this doing? To keep it  simple, when Python runs a file directly,  
it names it `__main__` and any code  beneath the `if` statement will only be run  
if the name of the file is `__main__`.
So when we run the test file it will have  the name `__main__` and this code won't run.  
But when we run this file it will have the  name `__main__` and it will run this code.
```python
if __name__ == "__main__":
    unittest.main()
```

---

Let’s also add this to our  test file and then try it out.
And we no longer see “True” in the output.
Okay, I’m going to change the True back to None, and delete our test in the test file 
and add back in the pass statement.
And we're all set up for the next video, in which we create a working function incrementally,
by creating tests which should initially fail, and then pass by adding code to our function.

## Building a function using TDD

we  can start writing the first of our tests.
One of the first items I want to test for is that  a TypeError is raised if a list is not passed into  
the function when it’s called. As mentioned in  the previous video, test functions need to start  
with the word ‘test’. If they don’t, they’ll be  ignored and won’t be run when we run our tests.  

- Let’s give our test a descriptive  name that details what it is testing,  
`test_throws_error_if_value_passed_in_is_not_list`,  and pass in a reference to self.
Inside our test, we write our assert  and I will use the assertRaises method.
This will call the assertRaises method  from TestCase and when the test is run  
it checks to see if a TypeError is raised  when the function is called with the value 4. 
This should fail, as our function  at the moment is set to return None.

```python
class TestEvens(unittest.TestCase):
    def test_throws_error_if_value_passed_in_is_not_list(self):
        self.assertRaises(TypeError, even_number_of_evens, 4)
```

Let’s run the test using the  command python3 test_evens.py.
We can see from the output that  it did fail and the reason given  
is that a TypeError wasn’t  raised by even_number_of_evens.
So we have a fail, which is what we  want initially when we create a test.  
We now need to write some code in our  function to get this test to pass.
I am going to add a check in our function  that checks if the value passed in is a list, 
and if it is, return True else raise a TypeError.
So I am going to replace the return statement,  
write an if else statement, use the isinstance()  method to check if the value “numbers” is a list  
and add a string to output  when the error is raised.

```python
def even_number_of_evens(numbers):
    """
    Should Raise a TypeError if a list in not passed into the function
    error message: "A list was not passed into the function"
    if the list is empty it will return False
    if the number of even numbers is odd - return False
    if the numner of even numbers is even - return True
    """

    if isinstance(numbers, list):
        return True
    else:
        raise TypeError("A list was not passed into the function")
```

So let’s save that and go back to  our test file and run the test again.  
This time we can see we get a pass, indicated  by the . and Ok at the end of the output.

So to recap what we have done, we  first wrote a test that should fail  
and then we wrote code in our  function so that our test passes.  
This is the red and green parts  of our red-green-refactor cycle.

The next test should test our  function returns False if an  
empty list is passed in, so I’ll create  a new test named test_values_in_list,  
and will use this code block  for the next few assertions.
I need to write an assertion  that checks if an empty list  
has been passed in and should be expecting False.
For this test I will use the assertEqual  method passing in the function with an  
empty list as an argument, and  the expected return of False.

```python
class TestEvens(unittest.TestCase):
    def test_throws_error_if_value_passed_in_is_not_list(self):
        self.assertRaises(TypeError, even_number_of_evens, 4)

    def test_values_in_list(self):
        self.assertEqual(even_number_of_evens([]), False)
```

And when we run the tests, it fails as expected.  
Again we need to add to the code in our  function, just enough to pass the test.
Let's pause so that you can think about what you  would need to add to the code in the function  
to pass this test. We will walk through  how I would do it when you get back.
Let’s look at how I got this test to pass.
Back in the function, I will replace  the return True with an if statement,  
which checks if numbers is equal to an  empty list and returns False if it is.
So let’s save the code and go back to  our test file and run the tests again.  

```python
def even_number_of_evens(numbers):
    """
    Should Raise a TypeError if a list in not passed into the function
    error message: "A list was not passed into the function"
    if the list is empty it will return False
    if the number of even numbers is odd - return False
    if the numner of even numbers is even - return True
    """

    if isinstance(numbers, list):
        if numbers == []:
            return False
    else:
        raise TypeError("A list was not passed into the function")
```

We can see from the output  that this has now passed.
So at this stage, you should understand the  process, which is you write a test that fails  
and then add code to the function  that should get the test to pass.
Our test passes for an empty list. What  should it do if we pass in two even numbers?  
In this case, we would want it to pass.
So let’s add another assert that should pass  when we add two even numbers to the list.
And when we run our test we see it fails.  
So, how do we get this to pass? Let’s add  an else to our if statement and return True.

```python
def even_number_of_evens(numbers):

    if isinstance(numbers, list):
        if numbers == []:
            return False
        else:
            return True
    else:
        raise TypeError("A list was not passed into the function")
```

This is probably not what you were expecting but  if we save our code and run the tests, we can see  
them all passing with flying colours. Looking at  the code in the function, it may seem that it does  
not make sense, but we are incrementally building  up the function by writing and passing tests.
Our function at the moment returns True for any  amount of numbers passed into it, and that's fine,  
but what is a test it should fail for? It should  fail if only one even number is passed in,  
so let's write a test that  checks for one even number.  
This test will fail and we can then look  at what we need to do to get it to pass.
Let’s run the tests. And as  expected this test fails.
We’re at the stage now where we need to  count the number of even numbers in the list 
and then check if that number itself is even.  So let's write the code to make this test pass.
If a number is sent in, let's initialize  a variable to say that we currently have zero evens.  
And now, let's write a for loop 
and within it an if statement that  checks if each number is even.
We can use the modulo operator to see if the  remainder when it's divided by two is zero. 
If it is, then it's an even number  and we increment the evens variable.
Outside the for loop, I’ll add a return  statement and using the modulo operator  
check if the evens variable is an even number.
So this will return True if the number  of evens is even, and False if it's not.

```python
def even_number_of_evens(numbers):

    if isinstance(numbers, list):
        if numbers == []:
            return False
        else:
            evens = 0

        for n in numbers:
            if n % 2 == 0:
                evens += 1

        return evens % 2 == 0
    else:
        raise TypeError("A list was not passed into the function")
```

Let's save that and run the tests again  
and see what we get. And we can  see that all tests are passing.
Things are looking good. Our function is  generally working, but there are still more  
tests because we haven't tested what will  happen if we send in any odd numbers yet. 


I’ll create another assert  so we can see what happens  
if we send in an odd number of odd numbers.
We would expect this to return  False but this time pass the test.  
Let's run our program.
It fails! That means that our program was returning True when it should have been returning False. 
Just have a look at the code for a  few minutes. See if you can figure  
out for yourself why the code is returning  True when it should be returning False. 
Well, as we see, the problem  is here with our return. 
Because we pass in 3 odd numbers, evens is going  to have the value 0 and 0 % 2 will equal 0,  
so True is returned. What we need to do here  
is add an if statement. We can use a truthy  falsy value check of evens, so if evens is > 0  
it will evaluate to True and False if it is 0 And within the if evens is greater than 0,  
we can return evens % 2 == 0.

```python
def even_number_of_evens(numbers):
    if isinstance(numbers, list):
        if numbers == []:
            return False
        else:
            evens = 0

        for n in numbers:
            if n % 2 == 0:
                evens += 1

        if evens:
            return evens % 2 == 0
        else:
            return False
    else:
        raise TypeError("A list was not passed into the function")
```

Now, when we run this, all tests are passed again.
We've used test-driven development to build  our function incrementally, and it works! 
It's not the prettiest, and it's maybe  not written using the cleanest code,  
but now that we know that it works.

## Refactoring

we are going to look at refactoring our code. Using the DRY, or Don't Repeat Yourself,  
principle, we can have a look at  our code and see if there's anything  
that's repetitive or redundant. 

One thing that stands out straight  
away is our check for an empty list right at the beginning of our code. 
As we step through the code, we can see that our check to see if evens equals 0 should cover that,  
so we can take out the empty list check. If we're wrong, then our tests will tell us. 
So, let's try that.
We can see that it still passes all the tests.
Another section of code that  stands out is this section here.
Anytime I see a for loop I tend to think of using  a list/dictionary comprehension, and this looks  
like a case to remove all these lines of code  and replace them with a list comprehension.
Let's look at how we could do that. I’ll  create a basic one and print it out,  
calling the function with the values [2, 1, 4].
If I run the file and we see [2, 1, 4] printed  out. Now, we don’t need the values.   
Looking at our code, we add 1 to the variable evens  each time we get an even number in the list.
Let’s replace the value with  1 for each item in the list.  
To do that, we replace the  first n with the number 1.
If we run our file, we get [1, 1, 1].
That’s better and more useful, but our code  uses an if statement to ignore odd numbers,  
so let’s add that to our  comprehension. That gives us:
1 for n in numbers if n % 2 == 0
If we run the code again, we get: [1,1] 
And finally, we can wrap the list comprehension  in the sum() method to get a total.
When we run the code again we get 2.
That works great, so we can  assign this to our evens variable  
and replace all those lines of code.
Another section I see we can  easily refactor is this section.
This looks like it should easily be  converted to a single line conditional expression
which would take the format: True if condition else False.
So let's try doing that.
For the condition I see I need two checks.  
First, we check if evens is not 0, so  let’s use a truthy check to do that.
Second, evens % 2 == 0, so lets add that as well.
And there we go: return True if evens  not 0 and evens % 2 == 0 else False.
Let’s see what happens if we run the tests again.
```python
def even_number_of_evens(numbers):
    """
    Should Raise a TypeError if a list in not passed into the function
    error message: "A list was not passed into the function"
    if the list is empty it will return False
    if the number of even numbers is odd - return False
    if the numner of even numbers is even - return True
    """

    if isinstance(numbers, list):
        evens = print(sum([1 for n in numbers if n % 2 == 0]))
        return True if evens and  evens % 2 == 0 else False
    else:
        raise TypeError("A list was not passed into the function")
```