# CodingSkillsInPython

I feel like you I know how to code in Pyhton, if I were asked to rate my level I would say a solid 6/10 or a good 7/10. (with all the modesty that coudl give you a scientific background)

I will start this repository to help myself improve my coding skills, for the purpose of becoming a better quant and put into practice my background in mathematics. 

## 1 - How the interpreter works 

### 1.1 - Namespaces

A namespace is a mapping from names to objects. Most namespaces are currently implemented as Python dictionaries. 
Examples of namespaces are: 
- the set of built-in names (containing functions such as abs(), and built-in exception names);
- the global names in a module;
- and the local names in a function invocation.
- In a sense the set of attributes of an object also form a namespace. 

Important : there is absolutely no relation between names in different namespaces; for instance, two different modules may both define a function $maximize$ without confusion — users of the modules must prefix it with the module name.

Strictly speaking, references to names in modules are attribute references: in the expression $modname.funcname$, $modname$ is a module object and $funcname$ is an attribute of it. In this case there happens to be a straightforward mapping between the module’s attributes and the global names defined in the module: they share the same namespace!

Attributes may be read-only or writable. In the latter case, assignment to attributes is possible. 
Module attributes are writable: you can write modname.the_answer = 42. Writable attributes may also be deleted with the del statement. 
For example, del modname.the_answer will remove the attribute the_answer from the object named by modname.

Namespaces are created at different moments and have different lifetimes. 
- The namespace containing the built-in names is created when the Python interpreter starts up, and is never deleted.
- The global namespace for a module is created when the module definition is read in; normally, module namespaces also last until the interpreter quits.
- The statements executed by the top-level invocation of the interpreter, either read from a script file or interactively, are considered part of a module called $__main__$, so they have their own global namespace.
- The local namespace for a function is created when the function is called, and deleted when the function returns or raises an exception that is not handled within the function. And, recursive invocations each have their own local namespace.

A scope is a textual region of a Python program where a namespace is directly accessible. “Directly accessible” here means that an unqualified reference to a name attempts to find the name in the namespace.

Although scopes are determined statically, they are used dynamically. At any time during execution, there are 3 or 4 nested scopes whose namespaces are directly accessible:
- the innermost scope, which is searched first, contains the local names
- the scopes of any enclosing functions, which are searched starting with the nearest enclosing scope, contain non-local, but also non-global names
- the next-to-last scope contains the current module’s global names
- the outermost scope (searched last) is the namespace containing built-in names

If a name is declared global, then all references and assignments go directly to the next-to-last scope containing the module’s global names. 
To rebind variables found outside of the innermost scope, the nonlocal statement can be used; if not declared nonlocal, those variables are read-only (an attempt to write to such a variable will simply create a new local variable in the innermost scope, leaving the identically named outer variable unchanged).


... to be completed{
Usually, the local scope references the local names of the (textually) current function. Outside functions, the local scope references the same namespace as the global scope: the module’s namespace. Class definitions place yet another namespace in the local scope.

It is important to realize that scopes are determined textually: the global scope of a function defined in a module is that module’s namespace, no matter from where or by what alias the function is called. On the other hand, the actual search for names is done dynamically, at run time — however, the language definition is evolving towards static name resolution, at “compile” time, so don’t rely on dynamic name resolution! (In fact, local variables are already determined statically.)

A special quirk of Python is that – if no global or nonlocal statement is in effect – assignments to names always go into the innermost scope. Assignments do not copy data — they just bind names to objects. The same is true for deletions: the statement del x removes the binding of x from the namespace referenced by the local scope. In fact, all operations that introduce new names use the local scope: in particular, import statements and function definitions bind the module or function name in the local scope.

The global statement can be used to indicate that particular variables live in the global scope and should be rebound there; the nonlocal statement indicates that particular variables live in an enclosing scope and should be rebound there.
}

## 2 - Objects, values and types. 

Objects are Python’s abstraction for data.
Every object has an identity, a type and a value :
  - An object’s identity never changes once it has been created; you may think of it as the object’s address in memory. The $is$ operator compares the identity of two objects; the $id()$ function returns an integer representing its identity.
  - An object’s type determines the operations that the object supports and also defines the possible values for objects of that type. The $type()$ function returns an object’s type (which is an object itself).

Like its identity, an object’s type is also unchangeable. The value of some objects can change. Objects whose value can change are said to be mutable; objects whose value is unchangeable once they are created are called immutable. An object’s mutability is determined by its type; for instance, numbers, strings and tuples are immutable, while dictionaries and lists are mutable.
