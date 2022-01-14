---
marp: true
headingDivider: 3
style: |
  section {
      font-size: 1.75rem
  }
---

# Elixir-Python Vocabulary

Elixir's syntax essentials for Python tourists

## Project goal

Help pythonistas navigate, **read** and understand **Elixir codebases**.

- can be used as lookup reference, just like a vocabulary
- each section contains an Elixir syntax feature and its python translation*
- provides links to official documentation 

\* *Warn*: translations are closest as possible and therefore not idiomatic

## What is **NOT**

- it's not a comprehensive tour of elixir features
- it's not a way to learn how to **write** Elixir code
- doesn't explain **how** things work in Elixir
- doesn't explain **why** Elixir is designed in such a way

If you are interested in those topics jump to ["Further Readings" section](#further-readings)


## Common syntax

```elixir
# this is a comment

"hello"  # string

[1, 2, 3]  # list

x = 1  # variable assignement

foo(bar)  # function call

1 + 1 == 2  # comparison operators 

not is_nil(x) and x > 0   # boolean operators 
```


## Atom

![auto](images/elixir_logo.png) Elixir
```elixir
:hello  
```

![auto](images/python_logo.png) Python
```python
HELLO = "hello"  # ~ global literal constant
```

Ref: https://hexdocs.pm/elixir/Atom.html


## Tuple

![auto](images/elixir_logo.png) Elixir
```elixir
{1, "b", :c}  
```

![auto](images/python_logo.png) Python
```python
(1, "b", C)  
```

Ref: https://hexdocs.pm/elixir/Tuple.html


## List

![auto](images/elixir_logo.png) Elixir
```elixir
[1, "b", :c]  # linked list [1 -> ["b" -> [:c]]]
```

![auto](images/python_logo.png) Python
```python
[1, "b", C]  # array list
```

Ref: https://hexdocs.pm/elixir/List.html


### List - Interaction examples

![auto](images/elixir_logo.png) Elixir
```elixir
x = [1, 2] ++ [3, 4] # (1) concatenate lists

y = [0 | x] # (2) prepend single element
```

![auto](images/python_logo.png) Python
```python
x = [1, 2] + [3, 4] # (1)

y = [0] + x  # (2) 
```

Ref: https://hexdocs.pm/elixir/List.html


## Keyword

![auto](images/elixir_logo.png) Elixir
```elixir
[{:a, 1}, {:b, 2}]  # list of pairs (atom, value)

[a: 1, b: 2]  # same as above with syntactic sugar
```

![auto](images/python_logo.png) Python
```python
[("a", 1), ("b", 2)]
```

Ref: https://hexdocs.pm/elixir/Keyword.html


## Map

![auto](images/elixir_logo.png) Elixir
```elixir
%{"a" => 1, "b" => 2} # (1) string keys

%{:a => 1, :b => 2} # (2) atom keys

%{a: 1, b: 2} # (3) same as (2) with syntactic sugar
```

![auto](images/python_logo.png) Python
```python
{"a": 1, "b": 2} # (1), (2) and (3)
```

Ref: https://hexdocs.pm/elixir/Map.html


### Map - Interaction examples

![auto](images/elixir_logo.png) Elixir
```elixir
x = Map.put(%{a: 1, b: 2}, :c, 3) # (1) add/update an element

x = %{x | c: 3} # (2) update an element (syntactic sugar)

y = Map.take(x, [:a, :b]) # (3) take a subset
```

![auto](images/python_logo.png) Python
```python
x = {**{"a": 1, "b": 2}, "c": 3} # (1) and (2)

y = {k: x[k] for k in x if k in ["a", "b"]} # (3)
```

Ref: https://hexdocs.pm/elixir/Map.html#summary


## If

![auto](images/elixir_logo.png) Elixir
```elixir
if x >= 0 do 
  :positive
else
  :negative
end

if x >= 0, do: :positive, else: :negative # shorthand
```

![auto](images/python_logo.png) Python
```python
"positive" if x >= 0 else "negative"
```

Ref: https://hexdocs.pm/elixir/Kernel.html#if/2


## Cond

![auto](images/elixir_logo.png) Elixir
```elixir
cond do # first true condition is entered
  x > 9000 -> "over 9000"
  x > 0 -> "meh"
  _ -> "do you even lift bro" # default branch
end
```

![auto](images/python_logo.png) Python
```python
if x > 9000:
  return "over 9000"
if x > 0: 
  return "meh"
return "do you even lift bro"
```

Ref: https://hexdocs.pm/elixir/Kernel.SpecialForms.html#cond/1


## Pattern matching

![auto](images/elixir_logo.png) Elixir
```elixir
{a, b, _} = {1, 2, 3}  # (1) a = 1, b = 2, don't care about third elem.

[a, ^b] = [1, 2]  # (2) a = 1 if second element == value of b (pin)

[head | tail] = [1, 2, 3]  # (3) head = 1, tail = [2, 3]

%{a: a} = %{a: 1, b: 2} # (4) a = 1 (~ destructuring)
```

![auto](images/python_logo.png) Python
```python
(a, b, _) = (1, 2, 3) # (1) 

[a, b] = [1, 2]; if b != 2: raise Exception("Match error!") # (2)

head, tail = lst[0], lst[1:]  # (3)

a = {"a": 1, "b": 2}["a"] # (4)
```

Ref: [getting-started#pattern-matching](https://elixir-lang.org/getting-started/pattern-matching.html)


## Case

![auto](images/elixir_logo.png) Elixir
```elixir
case result do # first pattern matched is entered
  {:ok, x} when rem(x, 2) -> {:odd, x}
  {:ok, x} -> {:even, x}
  _ -> :error
end
```

![auto](images/python_logo.png) Python
```python
if not isinstance(result, tuple): return "error"
if len(result) != 2: return "error"
if result[0] != "ok": return "error"

x = result[1]
return ("odd", x) if x % 2 else ("even", x)
```

Ref: https://hexdocs.pm/elixir/Kernel.SpecialForms.html#case/2


## With

![auto](images/elixir_logo.png) Elixir
```elixir
with {:ok, string} <- Map.fetch(map, :key), 
     {value, _} <- Integer.parse(string) do
     value
else # first failed match is sent here
  mismatch -> mismatch 
end
```

![auto](images/python_logo.png) Python
```python
if "key" not in map: return "error"
string = map["key"]
if not string.isnumeric(): return "error"
return int(string) 
```

Ref: https://hexdocs.pm/elixir/Kernel.SpecialForms.html#with/1 


## Function

![auto](images/elixir_logo.png) Elixir
```elixir
def add(x, y) do # (1) named function
  x + y # last expression is the return value
end

def add(x, y), do: x + y # (2) shorthand, same as (1)
defp add(x, y), do: x + y # (3) private function
```

![auto](images/python_logo.png) Python
```python
def add(x, y): # (1) and (2)
  return x + y

def _add(x, y): # (3)
  return x + y
```

Ref: https://hexdocs.pm/elixir/Kernel.html#def/2

### Function - Pattern matching

![auto](images/elixir_logo.png) Elixir
```elixir
# function definition can be splitted in branches
def op(:add, x, y), do: x + y
def op(:sub, x, y), do: x - y
def op(name, _, _), do: raise "Unknown operation #{name}"
```

![auto](images/python_logo.png) Python
```python
def op(name, x, y):
  if name == "add":
    return x + y
  if name == "sub":
    return x - y
  raise Exception(f"Unknown operation {name}")
```

Ref: https://hexdocs.pm/elixir/Kernel.html#def/2


### Function - Default parameters

![auto](images/elixir_logo.png) Elixir
```elixir
def increment(x, delta \\ 1), do: x + delta
```

![auto](images/python_logo.png) Python
```python
def increment(x, delta = 1):
  return x + delta
```

Ref: https://hexdocs.pm/elixir/Kernel.html#def/2


### Function - Keyword 

![auto](images/elixir_logo.png) Elixir
```elixir
# named parameters are (often) passed as keywords
String.split("a,b,c", ",", [{:parts, 2}]) # (1)

String.split("a,b,c", ",", parts: 2) # (2) same as (1) syntactic sugar
```

![auto](images/python_logo.png) Python
```python
"a,b,c".split(",", maxsplit=1) # (1) and (2)
```

Ref: https://hexdocs.pm/elixir/Kernel.html#def/2


## Lambda

![auto](images/elixir_logo.png) Elixir
```elixir
add = fn a, b -> a + b end

add.(1, 2) # note the "."!
```

![auto](images/python_logo.png) Python
```python
add = lambda x, y: x + y

add(1, 2)
```

Ref: https://hexdocs.pm/elixir/Kernel.SpecialForms.html#fn/1 


### Lambda - Shorthand

![auto](images/elixir_logo.png) Elixir
```elixir
add = &(&1 + &2) # (1) reference input parameters by positional index 

add = &Kernel.+/2 # (2) reference an existing function (name / arity)

add_one = &Kernel.+(&1, 1) # (3) ~ partial application
```

![auto](images/python_logo.png) Python
```python
add = lambda x, y: x + y # (1)

import operator
add = operator.add # (2)

add_one = lambda x: operator.add(x, 1) # (3)
```

Ref: https://hexdocs.pm/elixir/Kernel.SpecialForms.html#&/1


## Pipe

![auto](images/elixir_logo.png) Elixir
```elixir
x         # the previous expression
|> foo()  # is passed as first parameter
|> bar(y) # of the next one
```

![auto](images/python_logo.png) Python
```python
temp = foo(x)
bar(temp, y)
```

Ref: https://hexdocs.pm/elixir/Kernel.html#%7C%3E/2 


## Enum

![auto](images/elixir_logo.png) Elixir
```elixir
Enum.map(lst, &(&1 * &1)) # (1)

Enum.filter(lst, &(&1 > 0)) # (2)
```

![auto](images/python_logo.png) Python
```python
[x * x for x in lst] # (1)

[x for x in lst if x > 0] # (2)
```

Ref: https://hexdocs.pm/elixir/Enum.html


### Enum - Reduce

![auto](images/elixir_logo.png) Elixir
```elixir
Enum.reduce(lst, 0, fn x, acc -> x + acc end)
```

![auto](images/python_logo.png) Python
```python
acc = 0
for x in lst:
  acc = x + acc
```

Ref: https://hexdocs.pm/elixir/Enum.html


## Module

![auto](images/elixir_logo.png) Elixir
```elixir
defmodule Foo.Bar do # in file foo/bar.ex
  alias Other.Baz  # allows to refer to Baz without "Other."
  @delta 1         # define constant delta = 1
  def increment(x), do: Baz.f(x) + @delta
end
```

![auto](images/python_logo.png) Python
```python
# in file foo/bar.py
from other import baz
DELTA = 1
def increment(x):
  return baz.f(x) + DELTA
```

Ref: https://hexdocs.pm/elixir/Kernel.html#defmodule/2


## Struct

![auto](images/elixir_logo.png) Elixir
```elixir
defmodule User do
  defstruct [:name, :age]
end

john = %User{name: "John"} # basically equivalent to a map
```

![auto](images/python_logo.png) Python
```python
class User:
  def __init__(self, name=None, age=None):
    self.name = name
    self.age = age

john = User(name="John")
```

Ref: https://hexdocs.pm/elixir/Kernel.html#defstruct/1


## Typespec

![auto](images/elixir_logo.png) Elixir
```elixir
@type name :: String.t() | nil

@spec greet(name()) :: String.t() | :error
def greet(nil), do: :error
def greet(name), do: "Hello #{name}"
```

![auto](images/python_logo.png) Python
```python
Name = Optional[str]

def greet(name: Name) -> Union[str, Literal["error"]]:
  return f"Hello {name}" if name is not None else "error"
```

Ref: https://hexdocs.pm/elixir/typespecs.html


## Further readings

- [Elixir Getting Started](https://elixir-lang.org/getting-started/introduction.html)
- [Elixir in Action (Book)](https://www.manning.com/books/elixir-in-action-second-edition)
- [Exercism Elixir Track](https://exercism.org/tracks/elixir)