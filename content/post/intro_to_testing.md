+++
date = "2017-07-19T00:00:00"
draft = false
title = "An Introduction to Unit Testing"
section_id = 0
+++


Automated Software Testing is a discipline that every person who writes code professionally should practice. I will not argue the merits of testing here, because plenty of other people make very convincing arguments.


## Tools:
 There are a variety of testing frameworks that are offered for the different languages and frameworks that are used software engineers.

 - [JUnit] (http://junit.org/junit4/)  for Jvm languages
 - [Minitest](https://github.com/seattlerb/minitest) for Ruby
 - [Go Test](https://golang.org/pkg/testing/) for Go

 Each of these libraries/frameworks provides a functionality to create tests, run tests, and make assertions


## 3 Steps of a Test:

### 1: Arrange

Arrange is the step to create/load test data and create the conditions

### 2: Act

Act is the step where the code that is under test is executed.

### 3: Assert

Assert is the step where the result or side-effect of the code is checked



## Simple Java Example

```java
public class CalculatorTest{

  @Test
  public void calculatorAddTwoNumbers() {
    // Arrange Step
    Calculator calculator = new Calculator();

    // Act Step
    Integer result = calculator.add(5, 7)

    // Assert Step
    assertEquals("Result", 12, result);
  }
}

public class Calculator{
  public Integer add(Integer a, Integer b){
    return a + b;
  }
}

```

## Example with Rails

In this example we are testing a `Person` ActiveRecord object that should require a first name and a maiden name to be valid
```ruby
class PersonTest < ActiveSupport::TestCase

  test 'Empty person should not save' do
    # Arrange
    person = Person.new

    # Act and Assert on same line
    assert_not person.save
  end

  test 'Person with first and maiden name should save' do
    #Arrange
    person = Person.new(first_name: 'test', maiden_name: 'person')

    # Act and Assert on same line
    assert person.save
    # Multiple assertions
    assert_equal 'test', person[:first_name]
    assert_equal 'person', person[:maiden_name]
  end
end

class Person < ApplicationRecord
  validates :first_name, presence: true
  validates :maiden_name, presence: true
end

```