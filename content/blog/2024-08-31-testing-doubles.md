+++
title = "Testing with Doubles in RSpec"
+++

In my time at Turing we have had a heavy focus on test driven development. For the majority of what we have worked on we have had what I think are pretty straightforward architectures where testing is also fairly straight forward. Our models and methods we worked with had basic methods and structures. Testing in this type of scenario isn’t too complicated either, for example with a User model it isn’t difficult to simply create the user in the test setup using a typical syntax like

```rb
user1 = User.create(name: “example”, password: “password”, status: “beginner)

user1.promote

expect(user1.status).to be(“intermediate”)
```

In this scenario we can simply call methods and test them this way. Later on when learning about testing external api calls we started to learn about mocking. There’s a few reason that we do this, we don’t want to keep making calls to an external api that may be costing us money. We might want to test multiple parts of one call, it would end up being wasteful to keep making the same call. What I didn’t realize about mocking at first is that it can be really useful in other testing scenarios too.

There are many advantages to mocking, when we are developing with TDD an advantage with mocks is that we can ‘create’ the object we are wanting to test on before we actually have the class that we are testing. Even if that isn’t the case and we already have the class that we are testing, when our apps get more complicated and interdependent mocking in tests allow us to quickly set up our tests without worrying as much about setup.

RSpec has a built in way of doing this, doubles. Doubles are essentially a mock, and are simply a way thta we can create an object to stand in place for our real object we are testing. In RSpec one way we can use a double is the following

```rb
user = double(“user”)
```

in this line we create a double of the User class. This double is not a user itself but just a representation of the user. Since this double isn't a user itself it does not have any of the properties or methods of the user class, yet. We can do the following to give the double methods we want it to be able to respond to.

```rb
allow(user).to receive(:promote).and_return("intermediate")
```

This allows our user method to mock rthe behavior of a user recieving the promote method. In a situation where we are not concerned with testing that user method we don't really need that behavior to play out. Mocking the bhavior let's us focus on what we are really wanting to test. Another benefit is that if the method we are mocking is highly compute intesive or maybe makes large network and database calls, we can skip that for the time being. If we want to simulate different edge cases and error conditions this is a way we can set that up, creating the exact scenario we want.

When I first came across doubles I was very confused, it seemed like it wasn't actually testing anything, turns out I was focusing on the wrong part of the test. Now I see the value in being able to isolate test cases and get more granular with what we are testing. I look forward to implimenting this more in the future and hope that you were able to learn something too
