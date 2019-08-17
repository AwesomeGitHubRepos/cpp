# ([C++](Cpp.md)) [Shiny](CppShiny.md)

[Shiny](CppShiny.md) is a free [C++](Cpp.md)
[profiler](CppProfiler.md). It works under (amongst other)
[G++](CppGpp.md). I have not got it to work under [C++ Builder](CppBuilder.md).

## Using Shiny with C++ Builder

You cannot use [Shiny](CppShiny.md) in [C++ Builder](CppBuilder.md).

But you can use the [preprocessor](CppPreprocessor.md) to remove the
[Shiny](CppShiny.md) [macro's](CppMacro.md):

```
#ifndef _WIN32
  //If the program is not compiled under C++ Builder
  // just #include the Shiny header
  #include "..\..\Shiny\Shiny.h"
#else
  //If the program is compiled under C++ Builder
  // remove all macro's.
  #define PROFILE_FUNC() ((void)0)
  #define PROFILER_UPDATE() ((void)0)
  #define PROFILER_OUTPUT(x) ((void)0)
#endif
``` 

## Example

Suppose we want to compare the runtime speed of the [STL](CppStl.md)
[std::sort](CppStdSort.md) and [bubble sort](CppBubbleSort.md).

```
 #include <algorithm>
#include <iostream>
#include <iterator>
#include <vector>
//---------------------------------------------------------------------------
//From http://www.richelbilderbeek.nl/CppBubbleSort.htm
template <class T>
void BubbleSort(std::vector<T>& v)
{
  //Let the profiler include this function in its measurements
  PROFILE_FUNC();

  const int size = static_cast<int>(v.size());

  for(int i=0; i!=size-1; ++i)
  {
    for(int j=0; j!=size-i-1; ++j)
    {
      if(v[j] > v[j+1])
      {
        std::swap(v[j],v[j+1]);
      }
    }
  }
}
//---------------------------------------------------------------------------
//From http://www.richelbilderbeek.nl/CppQuickSort.htm
template <class T>
void QuickSort(std::vector<T>& v)
{
  //Let the profiler include this function in its measurements
  PROFILE_FUNC();

  std::sort(v.begin(),v.end());
}
//---------------------------------------------------------------------------
const std::vector<int> CreateVector(const int sz)
{
  //Let the profiler include this function in its measurements
  PROFILE_FUNC();

  std::vector<int> v(100);
  std::generate(v.begin(),v.end(),std::rand);
  return v;
}
//---------------------------------------------------------------------------
int main()
{
  const int n_runs = 10000;
  const int max_int = std::numeric_limits<int>::max();

  for (int i=0; i!=n_runs; ++i)
  {
    //Update the profiler
    PROFILER_UPDATE();
    //Create a std::vector of random integers
    const std::vector<int> v = CreateVector(max_int);
    //Bubble-sort a copy of this std::vector
    std::vector<int> v_bubble = v;
    BubbleSort(v_bubble);
    //Quicksort a copy of this std::vector
    std::vector<int> v_quick = v;
    QuickSort(v_quick);
  }
  //Write the profiler measurements to file
  PROFILER_OUTPUT("profiler.rtf");
}
```

Compile the program with for example:

```
g++ -o Main UnitMain.cpp ../../Shiny/ShinyManager.cpp ../../Shiny/ShinyNode.cpp ../../Shiny/ShinyNodePool.cpp ../../Shiny/ShinyTools.cpp ../../Shiny/ShinyOutput.cpp
```

Then run the program and the following text file (called profiler.rtf)
is created:

```
flat profile hits  self   time total time
<root>       0.0    31 us   3% 987 us 103%
CreateVector 1.0   274 ns   0% 274 ns   0%
BubbleSort   1.0   954 us 100% 954 us 100%
QuickSort    1.0     1 us   0%   1 us   0%

call tree    hits  self    time total time
<root>       0.0     31 us   3% 987 us 103%
CreateVector 1.0    274 ns   0% 274 ns   0%
BubbleSort   1.0    954 us 100% 954 us 100%
QuickSort    1.0      1 us   0%   1 us   0%
``` 

The program has spent 100% of 103% in the function BubbleSort and only
less then 0.5% in QuickSort. You have now measured that in this case
QuickSort is faster. This was just as expected for large std::vector
sizes.

## External links

 * [Shiny SourceForge website](http://sourceforge.net/projects/shinyprofiler)
 * [Shiny Google Code website](http://code.google.com/p/shinyprofiler)
