# ([C++](Cpp.md)) [stream](CppStream.md)

[Streams](CppStream.md) are like flexible flow-through
[containers](CppContainer.md).

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  int main() {   const bool b = true;   const char c = 'c';   const int i = 1;   const double d = 1.1;   std::cout     << "bool b: " << b << '\n'     << "char c: " << c << '\n'     << "integer i: " << i << '\n'     << "double d: " << d << std::endl; }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Screen output:


  ---------------------------------------------------
  ` bool b: 1 char c: c integer i: 1 double d: 1.1`
  ---------------------------------------------------



[Global](CppGlobal.md) [streams](CppStream.md)
------------------------------------------------

 

Examples of [global](CppGlobal.md) [streams](CppStream.md) are:

-   [std::cout](CppStdCout.md) (an [std::ostream](CppStdOstream.md))
-   [std::cin](CppStdCin.md) (an [std::istream](CppStdIstream.md))
-   [std::clog](CppStdClog.md) (an [std::ostream](CppStdOstream.md))
-   [std::cerr](CppStdCerr.md) (an [std::ostream](CppStdOstream.md))

[stream](CppStream.md) [(data) types](CppDataType.md)
-------------------------------------------------------

 

Types of [streams](CppStream.md) are:

-   [std::stringstream](CppStdStringstream.md): a
    [std::string](CppStdString.md) [stream](CppStream.md)
-   [std::ostream](CppStdOstream.md): output [stream](CppStream.md)
-   [std::istream](CppStdIstream.md): input [stream](CppStream.md)
-   [std::fstream](CppStdFstream.md): file [stream](CppStream.md)

[stream](CppStream.md) operations
----------------------------------

 

Things one can do on a [stream](CppStream.md):

-   [std::endl](CppStdEndl.md): adds newline ('\\n') and flushes the
    [stream](CppStream.md)
-   [std::ends](CppEnds.md): adds null ('\\0') to the
    [stream](CppStream.md)

[Stream](CppStream.md) format flags
------------------------------------

A [stream](CppStream.md) format flag is something that can be on or
off. [Stream](CppStream.md) format flags are:

-   std::ios::skipws: skip whitespace (on by default for input streams)
-   std::ios::showbase: indicate the numeric base
-   std::ios::showpoint: show decimal point and trailing zeroes for
    doubles
-   std::ios::uppercase: show uppercase characters in hex (ABCDEF) and
    scientific (E) notation
-   std::ios::showpos
-   std::ios::unitbuf

Turning a flag on and off is shown in the code below.

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  int main() {   std::cout << 1 << '\n';   std::cout.setf(std::ios::showpos);   std::cout << 1 << '\n';   std::cout.unsetf(std::ios::showpos);   std::cout << 1 << '\n'; }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


## [Stream](CppStream.md) flag field

A [stream](CppStream.md) flag field is a group of options of which only
one can be in effect, similar to a radiogroup control. To set a certain
option, one needs to clear the flag group field, then set the desired
option.

[Stream](CppStream.md) format flags are:

-   std::ios::basefield: std::ios::dec, std::ios::hex, std::ios::oct
-   std::ios::floatfield: std::ios::fixed, std::ios::scientific
-   std::ios::adjustfield: std::ios::left, std::ios::right,
    std::ios::internal

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  int main() {   //Turns on decimal notation,   //clears current notation (i.e. basefield)   std::cout.setf(std::ios::dec,std::ios::basefield);   std::cout << 15 << '\n';   //Turns on hexadecimal notation,   //clears current notation (i.e. basefield)   std::cout.setf(std::ios::hex,std::ios::basefield);   std::cout << 15 << '\n';   //Turns on octal notation,   //clears current notation (i.e. basefield)   std::cout.setf(std::ios::oct,std::ios::basefield);   std::cout << 15 << '\n'; }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## [Stream](CppStream.md) manipulators

[Stream](CppStream.md) manipulators are like [stream](CppStream.md)
formatting flags and formatting fields, except that manipulators are the
streamable version of flags and fields.

[Stream](CppStream.md) manipulators are:

-   [nl](CppNl.md)
-   [std::fixed](CppStdFixed.md)
-   [std::internal](CppStdInternal.md)
-   [std::left](CppStdLeft.md)
-   [std::noshowbase](CppStdNoshowbase.md)
-   [std::noshowpoint](CppStdNoshowpoint.md)
-   [std::noshowpos](CppStdNoshowpos.md)
-   [std::noskipws](CppStdNoskipws.md)
-   [std::nouppercase](CppStdNouppercase.md)
-   [std::resetiosflags](CppStdResetiosflags.md)
-   [std::right](CppStdRight.md)
-   [std::scientific](CppStdScientific.md)
-   [std::setbase](CppStdSetbase.md)
-   [std::setfill](CppStdSetfill.md)
-   [std::setiosflags](CppStdSetiosflags.md)
-   [std::setprecision](CppStdSetprecision.md)
-   [std::setw](CppStdSetw.md)
-   [std::showbase](CppStdShowbase.md)
-   [std::showpoint](CppStdShowpoint.md)
-   [std::showpos](CppStdShowpos.md)
-   [std::skipws](CppStdSkipws.md)
-   [std::uppercase](CppStdUppercase.md)

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  int main() {   //Turn on decimal notation   std::cout << std::dec << 15 << '\n';   //Turn on hexidecimal notation   std::cout << std::hex << 15 << '\n';   //Turn on octal notation   std::cout << std::oct << 15 << '\n'; }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## [stream](CppStream.md) code snippets

Some code snippets one can use when working witj
[stream](CppStream.md):

-   [Read and write a std::vector from/to a std::stream](CppVectorToStream.md)
-   [Write and read a std::vector to/from a std::stream](CppVectorToStream.md)
