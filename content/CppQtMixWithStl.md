
 

 

 

 

 

([C++](Cpp.md)) ![Qt](PicQt.png) [Mixing Qt with STL and Boost](CppQtMixWithStl.md)
=====================================================================================

 

This page is dedicated to answer the question if [Qt
Creator](CppQtCreator.md) mixes well with the [STL](CppStl.md) and
[Boost](CppBoost.md) libraries.

The conclusion is that they mix perfectly using the following operating
systems:

 

-   Ubuntu
-   Windows XP
-   Xubuntu

 

 

 

 

 

Ubuntu
------

 

Qt Creator mixes well with STL and Boost under Ubuntu.

 

 

 

 

 

### Installation under Ubuntu

 

No problems: download Boost and follow the instructions. Everything will
work as expected

 

 

 

 

 

Microsoft Windows XP, Service Pack 3
------------------------------------

 

Qt Creator mixes well with STL and Boost under Microsoft Windows XP with
Service Pack 3 installed.

 

 

 

 

 

### Installation under Microsoft Windows XP, Service Pack 3

 

No problem: copy the header files into the QT include folder.

 

 

 

 

 

### Use of assert under Microsoft Windows XP, Service Pack 3

 

If, in a QT4 GUI application, you use an assert statement that fails,
the application terminates and requests to send an error report to
Microsoft. In this error report, the failed assertion is hard to find.
When using Q\_ASSERT (and \#include &lt;qglobal.h&gt;) the same occurs.

 

 

 

 

 

Xubuntu
-------

 

Qt Creator mixes well with STL and Boost under Xubuntu.

 

 

 

 

 

### Installation under Xubuntu

 

No problems: download the STL and Boost with 'Synaptic' or another
application installation manager.

 

 

 

 

 

### Use of assert under Xubuntu

 

The assert statement that failed is written to the application output
window.

 

 

 

 

 

 

