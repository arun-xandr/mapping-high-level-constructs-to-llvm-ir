Lambda Functions
----------------

A lambda function is an anonymous function with the added spice that it
may freely refer to the local variables (including argument variables)
in the containing function. Lambdas are implemented just like Pascal's
nested functions, except the compiler is responsible for generating an
internal name for the lambda function. There are a few different ways of
implementing lambda functions (see `Wikipedia on Nested
Functions <en.wikipedia.org/wiki/Nested_function>`__ for more
information).

.. literalinclude:: listings/lambda_func_0.cpp
   :language: c++

Here the "problem" is that the lambda function references a local
variable of the caller, namely ``a``, even though the lambda function is
a function of its own. This can be solved easily by passing the local
variable in as an implicit argument to the lambda function:


.. literalinclude:: listings/lambda_func_0_cleaned.ll
   :language: llvm

Alternatively, if the lambda function uses more than a few variables,
you can wrap them up in a structure which you pass in a pointer to the
lambda function:

.. literalinclude:: listings/lambda_func_1.cpp
   :language: c++

Becomes:

.. literalinclude:: listings/lambda_func_1_cleaned.ll
   :language: llvm

Obviously there are some possible variations over this theme:

-  You could pass all implicit as explicit arguments as arguments.
-  You could pass all implicit as explicit arguments in the structure.
-  You could pass in a pointer to the frame of the caller and let the
   lambda function extract the arguments and locals from the input
   frame.
