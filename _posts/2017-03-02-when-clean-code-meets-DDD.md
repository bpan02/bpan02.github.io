During my flight to a training class this Saturday, I read the first few chapters in Domain-Driven Design: Tackling Complexity in the Heart of Software​.

In the first "Crunching Knowledge" chapter, it talks about how we can share the domain knowledge across the team in design and code.
In the old waterfall method, the business experts talk to the analysts, and analysts digest and abstract and pass the result along to the programmers, who code the software. This approach fails because it completely lacks feedback.

Other projects use an iterative process, but they fail to build up knowledge because they don't abstract.

Good programmers will naturally start to abstract and develop a model that can do more work.

It then shows an example to implement a requirement in the shipping domain: Allow 10% overbooking.
  public int MakeBooking(Cargo cargo, Voyage voyage)
        {
            var maxBooking = voyage.Capacity*1.1;
            if (voyage.BookedCargoSize + cargo.Size > maxBooking

)
                return -1;
            var confirmation = orderConfirmationSequence.Next();
            voyage.AddCargo(cargo, confirmation);
            return confirmation;
        }
‍
‍
The code smell here is that an important business rule is hidden as a guard clause in an application method.

This reminds me of how Clean Code should look like.
I always think of clean code as self-explanatory, easy to understand, easy to modify and easy to test.
Now I know there is something more: Clean code should also bring in business value.
It should try to close the feedback.
It should be able to be represented to business experts as technical artifacts, and business people understand the code by reading.

Consider the code below after abstracting the overbooking policy from the condition check.
 public int MakeBooking(Cargo cargo, Voyage voyage)
        {
            if (!overbookingPolicy.isAllowed(cargo, voyage))
                return -1;
            var confirmation = orderConfirmationSequence.Next();
            voyage.AddCargo(cargo, confirmation);
            return confirmation;
        }
‍
‍
Now as written, business expert could read the above code and verify the rule, and it is easy for developers to connect the requirement with the code as well.
When clean code meets DDD, good things happen.Programming Guild​
