# sfjie
Specs (= method pre- and postconditions) for Java in Eclipse

The goal of this project is to hack Eclipse's Java development tooling so that it supports editing and building programs that specify preconditions and postconditions for methods as boolean Java expressions inside comments, like so:
```java
class Account {

    private int balance;
    
    public int getBalance() { return balance; }
    
    public Account()
        //@ post getBalance() == 0;
    {}
    
    public void deposit(int amount)
        //@ pre 0 <= amount;
        //@ post getBalance() == old(getBalance()) + amount;
    {
        balance += amount;
    }
    
    public void withdraw(int amount)
        //@ pre 0 <= amount && amount <= getBalance();
        //@ post getBalance() == old(getBalance()) - amount;
    {
        balance -= amount;
    }

}
```
Edit-time support should include syntax highlighting, squigglies indicating malformed or ill-typed fragments, code completion, and refactoring. Build-time support should include optionally generating run-time checks. The hacked Eclipse should be suitable for use by students as part of their Java programming course.

It should be as easy as possible to keep the hacked Eclipse up-to-date with the upstream Eclipse, so as to incorporate work done upstream to support new Java language features, add new editor features, fix bugs, etc.
