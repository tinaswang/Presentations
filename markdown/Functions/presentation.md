# Good Practices for Functions


Ricardo M. Ferraz Leal

[rhf@ornl.gov](mailto:rhf@ornl.gov?subject=DbC)

---

# Design by Contract

- What does contract expect - `@precondition`
- What does contract guarantee? - `@postcondition`
- What does contract maintain? - `@invariant`

It is the caller's responsibility to make sure the pre-condition is met.

---

# PEP 0316 - Programming by Contract for Python

*Status:	Deferred*

# Alternatives:

- PyContract
- PyDBC
- decontractors

---

# DbC in Python

```python
from decontractors import *

@Precondition(lambda: x > 0 and y > 0)
@Postcondition(lambda: __return__ == (x + y))
def positive_nonzero_addition(x, y):
    # Try changing the expression to return something else
    return x + y

# Won't work if at least one parameter is negative or zero
print positive_nonzero_addition(4, 1)
```

---

# DbC in Python: Assertions do (part of) the job!

```python
def positive_nonzero_addition(x, y):
    assert x > 0, 'x must be positive!'
    assert y > 0, 'y must be positive!'
    return x + y

print positive_nonzero_addition(4, 1)
print positive_nonzero_addition(4, -1)
```
```
python -O <filename> # Turns assertions off!
```

---

# Law of Demeter

3 principles:

- Each unit should have only limited knowledge about other units: only units "closely" related to the current unit.
- Each unit should only talk to its friends; don't talk to strangers.
- Only talk to your immediate friends.

---

# Law of Demeter: Functions

The Law of Demeter for functions states that any method of an object should call only methods belong to:

```c++
class Demeter {
private:
  A *a;
  int func();
public:
  void example(B& b);
}
void Demeter::example(B& b) {
  C c;
  // itself
  int f = func();
  // any parameters that were passed in to the method
  b.invert();
  a = new A();
  // any objects created  
  a->setActive();
  // any directly held component objects
  c.print();
}
```

---

# Law of Demeter: Cons

The cost:

> You will be writing a large number of wrapper methods that simply forward the request on to a delegate.
>
> These wrapper methods will impose both a runtime cost and a space overhead, which may be significant—even prohibitive—in some applications.

---

# Let's KISS* for now.

**Plain English does the job:**

- Precondition:
  - What are valid parameters (ranges, types, etc)?
- Postcondition
  - What is supposed to be returned
- Invariants or Variants(?)
  - Any side effects I should be aware???
- Use ```assertions``` in the test/development environment.

In addition:

- Small functions (screen size maximum!)
- Write function intent
- Explain any choices made

[*]: "Keep it simple, stupid"
