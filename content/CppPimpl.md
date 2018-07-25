# ([C++](Cpp.md)) [Pimpl](CppPimpl.md)

[Pimpl](CppPimpl.md) is an abbreviation of '[pointer](CppPointer.md)
to [implementation](CppImplementation.md)'.

The idea of the [Pimpl](CppPimpl.md) idiom is to give a
[class](CppClass.md) (for example 'Lizard') an [opaque (smart)
pointer](CppOpaquePointer.md) to the actual
[implementation](CppImplementation.md) (for example 'LizardImpl'). The
[opaque (smart) pointer](CppOpaquePointer.md) enables it to do a
[forward declaration](CppForwardDeclaration.md) of the
[implementation](CppImplementation.md) [class](CppClass.md) only,
without the [compiler](CppCompiler.md) needing to know the actual
[type](CppDataType.md). This shortens build times [1]. All the
[public](CppPublic.md) [member functions](CppMemberFunction.md) of the
[Pimpl](CppPimpl.md) [class](CppClass.md) will (often) call the
[member functions](CppMemberFunction.md) of the
[implementation](CppImplementation.md) [class](CppClass.md) with the
same name.

The advantages of using the [Pimpl](CppPimpl.md) idiom are:

 * Shorten build times [1]
 * Remove visibility of [private](CppPrivate.md) [member
    functions](CppMemberFunction.md) [1]
 * Improved error handling and safety [1]

The disadvantage of using the [Pimpl](CppPimpl.md) idiom is the cost of
an extra level of indirection, so [Pimpl](CppPimpl.md) judiciously
[1].

## [Examples](CppExample.md)

 * [Pimpl example 1: Lizard implementation in multiple file using
    std::shared_ptr](CppPimplExample1.md)

Most lizards remain having the same gender for all their live.
Therefore, it is a good idea to make a lizard's gender a const member
variable. Problem is, that this makes a lizard class uncopyable. In this
example I solve this by making a Lizard contain an opaque pointer to
LizardImpl, where a LizardImpl does have a constant gender. Because I
want to be able to do a [shallow copy](CppShallowCopy.md) on Lizards, I
use a [boost::shared_ptr](CppBoostShared_ptr.md). Also note that the
code is very similar to a [Strategy](CppDesignPatternStrategy.md)
[design pattern](CppDesignPattern.md).


 

## lizard.h

```
#ifndef CPP_PIMPL_LIZARD_H
#define CPP_PIMPL_LIZARD_H

enum class Gender { male, female };

#include <memory>

class Lizard
{
public:
  Lizard(const Gender gender);
  ~Lizard();
  Gender GetGender() const noexcept;

private:
  struct LizardImpl;
  std::shared_ptr<LizardImpl> mPimpl;
};

#endif // CPP_PIMPL_LIZARD_H
```

## lizard.cpp

```
#include "CppPimplLizard.h"

struct Lizard::LizardImpl
{
  LizardImpl(const Gender gender);
  const Gender mGender;
};

Lizard::Lizard(const Gender gender)
  : mPimpl(std::make_shared<LizardImpl>(gender))
{

}

Lizard::~Lizard()
{
  //Need destructor definition in implementation file
}

Gender Lizard::GetGender() const noexcept
{
  return mPimpl->mGender;
}

Lizard::LizardImpl::LizardImpl(const Gender gender) : mGender(gender)
{

}
```

## [References](CppReferences.md)

 * [1] [Herb Sutter](CppHerbSutter.md), [Andrei Alexandrescu](CppAndreiAlexandrescu.md). 
   C++ coding standards: 101 rules, guidelines, and best practices. ISBN: 0-32-111358-6. 
   Item 43: 'Pimpl judiciously'.

