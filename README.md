# CPP17-RemovedConcepts
Removing the register Keyword,  Removing Deprecated operator++(bool), Removing Deprecated Exception Specifications, Removing Trigraphs

Removing the register Keyword

The register keyword was deprecated in 2011 (C++11), and it has had no meaning since
then. It was removed in C++17. The keyword is reserved and might be repurposed in future
revisions of the Standard (for example auto keyword was reused and now is an entirely
new and powerful feature).
If you use register to declare a variable:
register int a;
You might get the following warning (GCC8.1 below)
warning: ISO C++17 does not allow 'register' storage class specifier
or error in Clang (Clang 7.0)
error: ISO C++17 does not allow 'register' storage class specifier

Removing Deprecated operator++(bool)

The increment operator for bool has been already deprecated for a very long time! The
committee recommended against its use back in 1998 (C++98), but they only now finally
agreed to remove it from the language. Note that operator-- was never enabled for bool.
If you try to write the following code:
bool b;
b++;
You should get a similar error like this from GCC (GCC 8.1):
error: use of an operand of type 'bool' in 'operator++' is forbidden in C++17

Removing Deprecated Exception Specifications

In C++17, exception specification will be part of the type system (as discussed in the next
chapter about Language Clarification). However, the standard contains old and deprecated
exception specification that appeared to be impractical and unused.
For example:
void fooThrowsInt(int a) throw(int) {
printf_s("can throw ints\n");
if (a == 0)
throw 1;
}
Pay special attention to that throw(int) part.
The above code has been deprecated since C++11. The only practical exception declaration
is throw() which means - this code won’t throw anything. Since C++11 it’s been advised
to use noexcept.

For example in clang 4.0 you’ll get the following error:
error: ISO C++1z does not allow dynamic exception specifications
[-Wdynamic-exception-spec] note: use 'noexcept(false)' instead

Removing Trigraphs

Trigraphs are special character sequences that could be used when a system doesn’t support
7-bit ASCII (like ISO 646). For example ??= generated #, ??- produced ~. (All of C++’s basic
source character set fits in 7-bit ASCII). Today, trigraphs are rarely used, and by removing
them from the translation phase, the compilation process can be more straightforward. See
a table below with all the trighraps that were declared until C++17:
Trigraph Replacement
??= #
??( [
??< {
??/ \
??) ]
??> }
??’ ˆ
??! |
??- ~
