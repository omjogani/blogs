---
title: RSpec Testing Handbook
date: 2024-03-12 10:00:00 -500
categories: [handbooks, rspec-testing]
tags: [ruby-on-rails, testing]
---

The Book: Effective Testing with RSpec says....

> Well, The truth is that you can make software just fine without writing tests, and you can write test just fine without RSpec, so you'll be okay if you stop further. But if you decide to keep going, you'll discover something interesting: Writing tests with RSpec is a great way to get really good at making software.
> That's because RSpec isn't just a testing framework. It's a tool for learning how to think critically, patiently and systematically about the design of your code, and how to make software in a methodical way so you have confidence that it's well organized, clear and correct.

## Writing First Test with RSpec

Let's follow complete Test Driven Development with RSpec. Writing First Test with `bouncer_spec.rb`
in `spec` folder.

```ruby
require 'bouncer'

describe 'Bouncer' do
  it 'rejects xx from entering the venue' do
    b = Bouncer.new
    bounced = b.bounce('xx')
    expect(bounced).to be_truthy
  end
end
```

**describe**: It is a block which contain collections of related tests. It helps to modularize the test cases.
**it**: used to define test case. It describe specific behavior that will be fulfilled by code.
**context**: It used to provide additional context to the test case or collection of test case.

---

To pass above mentioned test we have to create a class Bouncer and It must satisfy the criteria provided in the test, so create expected method and it's return value in `bouncer.rb`.

```ruby
class Bouncer
  def bounce(bouncee)
    bouncee == 'xx'
  end
end
```

# Different Types of Matchers in RSpec

**eq()**

- It is used to check equality of variables but not for the objects.
  **be()**
- For the objects `be()` is used to check equality.

**Comparisons**
Sometimes, Instead of asserting for exact match, we want to assert on some condition. Following are the method to do the same.

```ruby
expect(actual).to be > expected
expect(actual).to be >= expected
expect(actual).to be < expected
expect(actual).to be >= expected
expect(actual).to be_between(minimum, maximum).inclusive # Value in range with minimum (default)
expect(actual).to be_between(minimum, maximum).exclusive # Value in range without minimum
expect(actual).to match(expression) # Compare Regular Expression
expect(actual).to be_within(delta).of(expected) # Good for floats
expect(actual).to start_with expected # Start with Certain Value
expect(actual).to end_with expected # End with Certain Value
```

**Truthiness and Existentialism**
In order to have clean and readable test we can use following methods.

```ruby
expect(actual).to be_truthy # pass if actual it truthy (not nil & false)
expect(actual).to be true # pass if actual == true
expect(actual).to be_falsey # pass if actual it falsey ( nil & false)
expect(actual).to be false # pass if actual == false
expect(actual).to be_nil # pass if actual is nil
expect(actual).to exist # pass if actual.exist?
expect(actual).to exist(*args) # pass if actual.exist?(*args)
```

**Expecting Errors**
In order to catch the error in the test case, We can utilize following methods.

```ruby
expect { ... }.to raise_error
expect { ... }.to raise_error(ErrorClass)
expect { ... }.to raise_error("message")
expect { ... }.to raise_error(ErrorClass, "message")
```

**Example 1** : Rook
`rook_spec.rb`

```ruby
require 'rook'

describe 'Rook' do
  it 'returns the correct points value' do
    rook = Rook.new
    rook_points = rook.points
    expect(rook_points).to be(5)
  end

  it 'returns the correct name' do
    rook = Rook.new
    rook_name = rook.name
    expect(rook_name).to be('Rook') # replace with eq('Rook')
  end

  it 'returns a point value greater than a pawns' do
    rook = Rook.new
    rook_points = rook.points
    expect(rook_points).to be > 1
  end
end
```

`rook.rb`

```ruby
class Rook
  def points
    5
  end

  def name
    "Rook"
  end
end
```

Based on above code, it seems like both test will pass. But Second test won't pass and the reason is `be()`. We're passing exactly same string as required by test but still be will also compare entire object with `equal?` method. Despite both objects having exact same value but their Id's are different hence Second Test will fail.

```bash
❯ irb
irb(main):001:0> "Rook".object_id
=> 9700
irb(main):002:0> "Rook".object_id
=> 20660
irb(main):003:0>
```

To solve this problem we can use `eq()` instead of `be()`. Because we're just interested in value we should utilize `eq()` instead.

**Example 2** : Player
`player_spec.rb`

```ruby
require 'player'

describe Player do
  it 'calculate the correct credits remaining' do
    player = Player.new
    player.credits = 1.5
    player.sub_credits(1.3)
    expect(player.credits).to be_within(0.0001).of 0.19999
  end

  it 'returns the correct value for the players active status' do
    player = Player.new
    player.active = "YES"
    expect(player.active).to be_truthy
  end

  it 'returns an error when sub_credits is passed a zero credit value' do
    player = Player.new
    player.credits = 2
    expect { player.sub_credits(0) }.to raise_exception(StandardError)
  end
end
```

`player.rb`

```ruby
class Player
  attr_accessor :credits
  attr_accessor :active

  def sub_credits(sub_cred)
    if sub_cred == 0
      raise StandardError
    end
    @credits -= sub_cred
  end
end
```

In `Player` Test, `be_within(0.10000).of 0.19999` means We expect the number of credits to be very close to 0.19999, but it can be a tiny bit off (up to 0.0001 more or less).
In Second Test all the values are truthy expect "False and nil". In Third Test Case It is expecting a Standard Exception to be thrown.

## Request Specs for Controllers

Request Spec provide RSpec wrapper for integration test of our rails application. Earlier we used to test actions of controller with `method: controller()` but it's not recommended now, the better way is Request Specs.
We assume our app as black box and we fire GET, POST, PATCH, PUT, DELETE request and we assert the response with status code or certain consequences. eg. POST method incremented count of records by one, etc.

`request/todos_spec.rb`

```ruby
require 'rails_helper'

RSpec.describe "Todos", type: :request do
  let(:todo) { { title: "New Todo", description: "This is new todo", is_done: false } }
  describe "GET /index" do
    it "returns http success" do
      get todo_index_path
      expect(response).to have_http_status(:success)
    end
  end
  describe 'GET /show' do
    it 'show specific todo' do
      todo = Todo.create(title: "Complete the task", description: "This is the description of task", is_done: false)
      get todo_show_url(todo)
      expect(response).to have_http_status(200)
    end
  end
  describe 'POST /create' do
    let(:todo_invalid) { { title: nil, description: "This is new todo", is_done: false } }

    it 'should add new Todo' do
      expect { post todo_create_url, params: { todo: todo } }.to change(Todo, :count).by(1)
    end

    it 'should not add new Todo with invalid params' do
      expect { post todo_create_url, params: { todo: todo_invalid } }.to change(Todo, :count).by(0)
    end

    it 'should redirect to todos page' do
      post todo_create_url, params: { todo: todo }
      expect(response).to redirect_to(todo_index_url)
    end

    it 'should not add todo in case of invalid data' do
      post todo_create_url, params: { todo: todo_invalid }
      expect(response).to have_http_status(:unprocessable_entity)
    end
  end
  describe 'PATCH /update' do
    let(:todo) { { title: "This is title!", description: "This is Updated Description!", is_done: false } }
    let(:todo_updated) { { title: "This is updated!", description: "This is Updated Description!", is_done: true } }
    let(:invalid_todo_updated) { { title: nil, description: "This is Updated Description!", is_done: true } }

    before(:each) do
      @todo_obj = Todo.create! todo
    end

    it 'should update todo with valid params' do
      patch todo_update_url(@todo_obj), params: { todo: todo_updated }
      @todo_obj.reload

      expect(response).to redirect_to(todo_update_url)
      expect(@todo_obj.title).to eq("This is updated!")
      expect(@todo_obj.description).to eq("This is Updated Description!")
      expect(@todo_obj.is_done).to be(true)
    end

    it 'should not update todo with invalid params' do
      patch todo_update_url(@todo_obj), params: { todo: invalid_todo_updated }
      @todo_obj.reload

      expect(response).to have_http_status(422)
    end
  end
  describe 'DELETE /destroy ' do
    before(:each) do
      @todo_created = Todo.create! todo
    end
    it 'should remove todo if todo_id is valid' do
      expect { delete todo_delete_url(@todo_created) }.to change(Todo, :count).by(-1)
    end

    it 'should redirect to index page after successful deletion of Todo' do
      delete todo_delete_url(@todo_created)
      expect(response).to redirect_to(todo_index_url)
    end

    it 'should not remove todo if todo_id is invalid' do
      invalid_todo_id = -1
      expect { delete todo_delete_url(invalid_todo_id) }.to raise_error(ActiveRecord::RecordNotFound, "Couldn't find Todo with 'id'=-1")
    end
  end
end
```

## Custom Matcher

Generally, When we deal with complex data structure which requires some pre-processing stuff at that time we use custom matchers. Here is the example of Custom Matcher.
`board.rb`

```ruby
class Board
  def total_pieces
    return 32
  end
end
```

`custom_matcher.rb`

```ruby
module CustomMatcher
  class OurCustomMatcher
    def initialize(target)
      @target = target
    end
    def matches?(value)
      value == @target
    end

    def failure_message
      'Out matcher failed to match'
    end
  end
  def self.custom_matcher(target)
    OurCustomMatcher.new(target)
  end
end
```

`board_spec.rb`

```ruby
require 'board'
require 'custom_matcher'

describe Board do
  describe '#total_pieces' do
    it 'has a total of 32 pieces' do
      b = Board.new
      expect(b.total_pieces).to CustomMatcher.custom_matcher(32)
    end
  end
end
```

While Implementing Custom Matcher we're required to implement 2 methods `matches?` and `failure_message`. Because when test case trying to compare it uses `matches?` method and in case of failure it looks for `failure_message` method.

## Let & Before Hooks

Example
`sandwich.rb`

```ruby
class Sandwich
  attr_accessor :meat, :cheese, :condiments
  def initialize(meat, cheese, condiments)
    self.meat = meat
    self.cheese = cheese
    self.condiments = condiments
  end
end
```

`sandwich_spec.rb`

```ruby
require 'sandwich'

describe Sandwich do
  context 'when the sandwich should be vegan' do
    it 'should not have meat' do
      sandwich = Sandwich.new(false, false, ['lettuce', 'tomato', 'mustard'])
      expect(sandwich.meat).to eq(false)
    end

    it 'should not have cheese' do
      sandwich = Sandwich.new(false, false, ['lettuce', 'tomato', 'mustard'])
      expect(sandwich.cheese).to eq(false)
    end

    it 'should not have mayonnaise' do
      sandwich = Sandwich.new(false, false, ['lettuce', 'tomato', 'mustard'])
      expect(sandwich.condiments).to_not include('mayonnaise')
    end
  end
end
```

As per the above code, We can observe that there are many duplication of the code and that's not good code. We want to reduce duplication of the code as much as we can.
We can reduce code duplication using **let** and **before** block. Here is the example

```ruby
require 'sandwich'

describe Sandwich do
  context 'when the sandwich should be vegan' do
  let(:sandwich) { Sandwich.new(false, false, ['lettuce', 'tomato', 'mustard']) }
    it 'should not have meat' do
      expect(sandwich.meat).to eq(false)
    end

    it 'should not have cheese' do
      expect(sandwich.cheese).to eq(false)
    end

    it 'should not have mayonnaise' do
      expect(sandwich.condiments).to_not include('mayonnaise')
    end
  end
  context 'when the sandwich should not be vegan' do
    before(:each) do
      @sandwich = Sandwich.new(true, true, ['lettuce', 'tomato', 'mayonnaise'])
    end

    it 'should have meat' do
      expect(@sandwich.meat).to be true
    end
    it 'should have cheese' do
      expect(@sandwich.cheese).to be true
    end
    it 'should have mayonnaise' do
      expect(@sandwich.condiments).to include('mayonnaise')
    end
  end
end
```

There are 2 different types of `let` in RSpec.

```ruby
let(:symbol) { ... }
```

Let is only available to test where It used. In other test where It is not used, It won't available there anyhow.

```ruby
let!(:symbol) { ... }
```

Let with exclamation is by default available to all the block weather you used that variable or not, doesn't matter it's available for all the blocks.
As per the requirement or scenario we can make use of either `let()` or `let!()`.

## Mocking in RSpec

Mocking is a technique to clone the behavior of objects and method temporarily. There are some reason we are required to clone the behavior.

1. Focus on current test instead of dependencies associated with the code.
2. When outcome is non-deterministic value such as random function.
3. To avoid invoking code which degrade the performance of the test.

There are few techniques of mocking.

1. Test Doubles
2. Method Stubs
3. Message Expectations

### RSpec Test Doubles

Test Doubles are used to mimic the behavior of the actual method. Test Doubles are typically used when we want to isolate the behavior of method it can be dependency over other method or any. Here is the example...
`car.rb`

```ruby
class Car
  attr_accessor :fuel_level
  def initialize(fuel)
    @fuel_level = fuel
  end

  def fill_up(pump)
    @fuel_level = pump.dispense_fuel
  end
end

class Pump
  def dispense_fuel
    10
  end
end
```

`car_spec.rb`

```ruby
require 'car'

describe Car do
  describe '#full_up' do
    it 'the car should have maximum fuel' do
      c = Car.new(50)
      p = double("Pump", dispense_fuel: 100)

      c.fill_up(p)
      expect(c.fuel_level).to eq(100)
    end
  end
end
```

While `dispense_fuel` returns 10 in `car.rb` and we're expecting 100 it would still pass. That's because of **double**. It mimics the behavior of `dispense_fuel` method and return the value specified in the test.
It sometimes leads to several issues. Let's say you made some changes in Pump such that It impacts the Car but still all the test of the Car will pass and bugs or issue will be negated. Suppose If `dispense_fuel` method is not exist then also test won't complain it will still pass. That's why we have to be cautious while using `test double`.

### Method Stubs

Method Stubbing is a technique to return a known value in response to a message. It can replace either existing method or methods which are not even exist. It can be implemented using **allow()** and **receive()** method.
`car.rb`

```ruby
class Car
  attr_accessor :fuel_level
  def initialize(fuel)
    @fuel_level = fuel
  end

  def fill_up(pump)
    @fuel_level = pump.dispense_fuel
  end
end

class Pump
  def dispense_fuel
    10
  end
end
```

`car_spec.rb`

```ruby
require 'car'

describe Car do
  describe '#fill_up' do
    it 'the car should have maximum fuel' do
      c = Car.new(50)
      p = Pump.new

      allow(p).to receive(:dispense_fuel).and_return(100)

      c.fill_up(p)
      expect(c.fuel_level).to eq(100)
    end
  end
end
```

In above example, it will mock the behavior of `dispense_fuel()` method and return 100 instead of calling actual method. `and_return()` is optional, if you provide it will return provided value otherwise it will return nil.

`allow()` is not consider as strict matcher because even stubbed object or method is not invoked, it would ignore that. But sometimes we also make sure that stubbed object or method is getting invoked that's where we use `expect()` instead of `allow()`.

### Example

```ruby
# Change
# FROM => @fuel_level = pump.dispense_fuel
# TO => @fuel_level = 100

def fill_up(pump)
  @fuel_level = 100
end
```

Still, if you run above test case it would pass. because allow() is not taking care about weather stubbed method is getting invoked or not. It just work.

### Message Expectations

Message Expectation states an expectation that an object should receive a specific message before completion of that specific test case.
It is like strict matcher because once you define some expectation which must be satisfied before exiting from that test case. If it failed to satisfy the expectation, test case will going to fail.
We can solve above issue mentioned in Method Sub's Example where we must have to make sure that `dispense_fuel()` is invoked.
`car.rb`

```ruby
class Car
  attr_accessor :fuel_level
  def initialize(fuel)
    @fuel_level = fuel
  end

  def fill_up(pump)
    @fuel_level = pump.dispense_fuel
  end
end

class Pump
  def dispense_fuel
    10
  end
end
```

`car_spec.rb`

```ruby
require 'car'

describe Car do
  describe '#fill_up' do
    it 'car should have maximum fuel' do
      c = Car.new(50)
      p = Pump.new
      expect(p).to receive(:dispense_fuel).and_return(100)

      c.fill_up(p)
      expect(c.fuel_level).to eq(100)
    end
  end
end
```

Now, We're forced to call the method `pump.dispense_fuel()`, otherwise test will fail. and When we satisfy the requirement we're good to go.
Additionally we can have some method to check more stuff as following...

```ruby
allow(p).to receive(:dispense_fuel).at_least(:once).and_return(100)

expect(p).to receive(:dispense_fuel).exactly(1).times.and_return(100)

# value specified in with denotes argument of dispense_fuel
expect(p).to receive(:dispense_fuel).with(true).and_return(100)

# just check involvement
expect(article).to receive(:title_length).and_call_original
```
