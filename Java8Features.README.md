## Why variable used in lambda expression should be final or effectively final?

Java 8 has a new concept called **Effectively final** variable. It means that a non-final local variable whose value never changes after initialization is called **Effectively Final**.

**This concept was introduced because prior to Java 8, we could not use a non-final local variable in an anonymous class**. If you wanna have access to a local variable in anonymous class, you have to make it final.

When lambda was introduced, this restriction was eased. Hence to the need to make local variable final if it’s not changed once it is initialized as lambda in itself is nothing but an anonymous class.

Java 8 realized the pain of declaring local variable final every time a developer used lambda, introduced this concept, and made it unnecessary to make local variables final. So if you see the rule for anonymous classes has not changed, it’s just you don’t have to write the final keyword every time when using lambdas.

