# ([C++](Cpp.md)) [GetAngle](CppGetAngle.md)
 

[GetAngle](CppGetAngle.md) is a [geometry](CppGeometry.md) [code
snippet](CppCodeSnippets.md) to calculate the angle between two
coordinats. All it needs is the distance between these two coordinats.
The resulting angle will be in the range \[0.0, 2.0 \* pi\], these
angles ordered like a clock:

```
12 o'clock is 0.0 * pi
 3 o'clock is 0.5 * pi
 6 o'clock is 1.0 * pi
 9 o'clock is 1.5 * pi
``` 

[GetAngle](CppGetAngle.md) is maintained in the
[CppGeometry](CppGeometry.md) [class](CppClass.md), see
[CppGeometry](CppGeometry.md) for the heavily tested, debugged and used
version.

## [GetAngle](CppGetAngle.md) using the [STL](CppStl.md) only

```c++
#include <cmath>

///Obtain the angle in radians between two deltas
///12 o'clock is 0.0 * pi
/// 3 o'clock is 0.5 * pi
/// 6 o'clock is 1.0 * pi
/// 9 o'clock is 1.5 * pi
//From www.richelbilderbeek.nl/CppGetAngle.htm
double GetAngle(const double dx, const double dy)
{
  return M_PI - (std::atan2(dx, dy));
}
```

## [GetAngle](CppGetAngle.md) using [Boost.Units](CppUnits.md)

Now the resulting angle has a unit.

```c++
#include <cmath>
#include <boost/units/systems/si.hpp>
#include <boost/units/base_units/angle/radian.hpp>

///Obtain the angle between two deltas
///12 o'clock is 0.0 * pi
/// 3 o'clock is 0.5 * pi
/// 6 o'clock is 1.0 * pi
/// 9 o'clock is 1.5 * pi
//From www.richelbilderbeek.nl/CppGetAngle.htm
const boost::units::quantity<boost::units::si::plane_angle> GetAngle(
  const boost::units::quantity<boost::units::si::length>& dx,
  const boost::units::quantity<boost::units::si::length>& dy)
{
  return boost::units::quantity<boost::units::si::plane_angle>(
    (M_PI - std::atan2(dx.value(),dy.value())) * boost::units::si::radians);
}
```

## Old version of GetAngle


This version I concluded at around the age of twelve (in GW-BASIC), so I
keep it in for nostalgic purposes.

```c++
#include <cassert>
#include <cmath>

//From www.richelbilderbeek.nl/CppGetAngle.htm
double GetAngle(const double dX, const double dY)
{
  //In which quadrant are we?
  if (dX > 0.0)
  {
    if (dY > 0.0)
    {
      //dX > 0.0 && dY > 0.0
      //Quadrant IV
      assert(dX > 0.0 && dY > 0.0);
      const double angle = (1.0 * M_PI) - std::atan(dX / dY);
      assert(angle > 0.5 * M_PI && angle < 1.0 * M_PI);
      return angle;
    }
    else if (dY < 0.0)
    {
      //dX > 0.0 && dY <= 0.0
      //Quadrant I
      assert(dX > 0.0 && dY < 0.0);
      const double angle = (0.0 * M_PI) - std::atan(dX / dY);
      assert(angle > 0.0 * M_PI && angle < 0.5 * M_PI);
      return angle;
    }
    else
    {
      //dX > 0.0 && dY == 0.0
      //On Y-axis, right side
      assert(dX > 0.0 && dY == 0.0);
      const double angle = 0.5 * M_PI;
      return angle;
    }
  }
  else if (dX < 0.0)
  {
    if (dY > 0.0)
    {
      //dX < 0.0 && dY > 0.0
      //Quadrant III
      assert(dX < 0.0 && dY > 0.0);
      const double angle = (1.0 * M_PI) - std::atan(dX / dY);
      assert(angle > 1.0 * M_PI && angle < 1.5 * M_PI);
      return angle;
    }
    else if (dY < 0.0)
    {
      //dX < 0.0 && dY < 0.0
      //Quadrant II
      assert(dX < 0.0 && dY < 0.0);
      const double angle = (2.0 * M_PI) - std::atan(dX / dY);
      assert(angle > 1.5 * M_PI && angle < 2.0 * M_PI);
      return angle;
    }
    else
    {
      //dX < 0.0 && dY == 0.0
      //On X-axis
      assert(dX < 0.0 && dY == 0.0);
      const double angle = 1.5 * M_PI;
      return angle;
    }
  }
  else
  {
    if (dY > 0.0)
    {
      //dX == 0 && dY > 0.0)
      //On Y-axis, right side of origin
      assert(dX==0.0 && dY > 0.0);
      const double angle = 1.0 * M_PI;
      return angle;
    }
    else if (dY < 0.0)
    {
      //dX == 0 && dY < 0.0)
      //On Y-axis, left side of origin
      assert(dX==0.0 && dY < 0.0);
      const double angle = 0.0 * M_PI;
      return angle;
    }
    else
    {
      //dX == 0.0 && dY == 0.0)
      //On origin
      assert(dX==0.0 && dY == 0.0);
      const double angle = 0.0 * M_PI;
      return angle;
    }
  }
}
```

## Testing [GetAngle](CppGetAngle.md)

 * [Download the Qt Creator project 'CppGetAngle' (zip)](CppGetAngle.zip)

```c++
#include <cassert>
#include <cmath>
#include <iostream>

///Obtain the angle in radians between two deltas
///12 o'clock is 0.0 * pi
/// 3 o'clock is 0.5 * pi
/// 6 o'clock is 1.0 * pi
/// 9 o'clock is 1.5 * pi
//From www.richelbilderbeek.nl/CppGetAngle.htm
double GetAngleOld(const double dX, const double dY)
{
  //In which quadrant are we?
  if (dX > 0.0)
  {
    if (dY > 0.0)
    {
      //dX > 0.0 && dY > 0.0
      //Quadrant IV
      assert(dX > 0.0 && dY > 0.0);
      const double angle = (1.0 * M_PI) - std::atan(dX / dY);
      assert(angle > 0.5 * M_PI && angle < 1.0 * M_PI);
      return angle;
    }
    else if (dY < 0.0)
    {
      //dX > 0.0 && dY <= 0.0
      //Quadrant I
      assert(dX > 0.0 && dY < 0.0);
      const double angle = (0.0 * M_PI) - std::atan(dX / dY);
      assert(angle > 0.0 * M_PI && angle < 0.5 * M_PI);
      return angle;
    }
    else
    {
      //dX > 0.0 && dY == 0.0
      //On Y-axis, right side
      assert(dX > 0.0 && dY == 0.0);
      const double angle = 0.5 * M_PI;
      return angle;
    }
  }
  else if (dX < 0.0)
  {
    if (dY > 0.0)
    {
      //dX < 0.0 && dY > 0.0
      //Quadrant III
      assert(dX < 0.0 && dY > 0.0);
      const double angle = (1.0 * M_PI) - std::atan(dX / dY);
      assert(angle > 1.0 * M_PI && angle < 1.5 * M_PI);
      return angle;
    }
    else if (dY < 0.0)
    {
      //dX < 0.0 && dY < 0.0
      //Quadrant II
      assert(dX < 0.0 && dY < 0.0);
      const double angle = (2.0 * M_PI) - std::atan(dX / dY);
      assert(angle > 1.5 * M_PI && angle < 2.0 * M_PI);
      return angle;
    }
    else
    {
      //dX < 0.0 && dY == 0.0
      //On X-axis
      assert(dX < 0.0 && dY == 0.0);
      const double angle = 1.5 * M_PI;
      return angle;
    }
  }
  else
  {
    if (dY > 0.0)
    {
      //dX == 0 && dY > 0.0)
      //On Y-axis, right side of origin
      assert(dX==0.0 && dY > 0.0);
      const double angle = 1.0 * M_PI;
      return angle;
    }
    else if (dY < 0.0)
    {
      //dX == 0 && dY < 0.0)
      //On Y-axis, left side of origin
      assert(dX==0.0 && dY < 0.0);
      const double angle = 0.0 * M_PI;
      return angle;
    }
    else
    {
      //dX == 0.0 && dY == 0.0)
      //On origin
      assert(dX==0.0 && dY == 0.0);
      const double angle = 0.0 * M_PI;
      return angle;
    }
  }
}

#include <cmath>

///Obtain the angle in radians between two deltas
///12 o'clock is 0.0 * pi
/// 3 o'clock is 0.5 * pi
/// 6 o'clock is 1.0 * pi
/// 9 o'clock is 1.5 * pi
//From www.richelbilderbeek.nl/CppGetAngle.htm
double GetAngleRadians(const double dx, const double dy)
{
  return M_PI - (std::atan2(dx,dy));
}


#include <cmath>
#include <boost/units/systems/si.hpp>
#include <boost/units/base_units/angle/radian.hpp>
///Obtain the angle between two deltas
///12 o'clock is 0.0 * pi
/// 3 o'clock is 0.5 * pi
/// 6 o'clock is 1.0 * pi
/// 9 o'clock is 1.5 * pi
//From www.richelbilderbeek.nl/CppGetAngle.htm
const boost::units::quantity<boost::units::si::plane_angle> GetAngle(
  const boost::units::quantity<boost::units::si::length>& dx,
  const boost::units::quantity<boost::units::si::length>& dy)
{
  return boost::units::quantity<boost::units::si::plane_angle>(
    (M_PI - std::atan2(dx.value(),dy.value())) * boost::units::si::radians);
}

#include <tuple>
#include <map>
#include <boost/units/io.hpp>

int main()
{
  using boost::units::quantity;
  using boost::units::si::length;
  using boost::units::si::meter;
  using boost::units::si::plane_angle;
  using boost::units::si::radians;

  //Test the functions
  //Create a table of (dx,dy) and the expected angle
  const std::vector<std::tuple<double,double,double> > v
    =
    {
      std::make_tuple( 0.0,-1.0, 0.00 * M_PI), //N
      std::make_tuple( 1.0,-1.0, 0.25 * M_PI), //NE
      std::make_tuple( 1.0, 0.0, 0.50 * M_PI), //E
      std::make_tuple( 1.0, 1.0, 0.75 * M_PI), //SE
      std::make_tuple( 0.0, 1.0, 1.00 * M_PI), //S
      std::make_tuple(-1.0, 1.0, 1.25 * M_PI), //SW
      std::make_tuple(-1.0, 0.0, 1.50 * M_PI), //W
      std::make_tuple(-1.0,-1.0, 1.75 * M_PI)  //NW
    };
  std::for_each(v.begin(),v.end(),
    [](const std::tuple<double,double,double>& t)
    {
      {
        //Test GetAngleRadians
        const double angle =  GetAngleRadians(std::get<0>(t),std::get<1>(t));
        const double expected = std::get<2>(t);
        assert(std::abs(angle-expected) < 0.01);
      }
      {
        //Test GetAngleRadiansOld
        const double angle =  GetAngleOld(std::get<0>(t),std::get<1>(t));
        const double expected = std::get<2>(t);
        assert(std::abs(angle-expected) < 0.01);
      }
      {
        //Test GetAngle
        using boost::units::si::length;
        using boost::units::si::meter;
        using boost::units::si::radians;
        using boost::units::quantity;
        using boost::units::si::plane_angle;

        const quantity<plane_angle> angle(
          GetAngle(
            std::get<0>(t) * meter,
            std::get<1>(t) * meter
          ));
        const quantity<plane_angle> expected(
          std::get<2>(t) * radians);
        assert(std::abs(angle.value()-expected.value()) < 0.01);
      }

    }
  );
  //Display
  for (double y = -1.0; y < 1.0; y+=0.21)
  {
    for (double x = -1.0; x < 1.0; x+=0.21)
    {
      const quantity<length> lx(x * meter);
      const quantity<length> ly(y * meter);

      std::cout << "(" << x << "," << y << "): "
        << GetAngleOld(x,y)
        << " or " << GetAngleRadians(x,y)
        << " or " << GetAngle(lx,ly) << '\n';
    }
  }
}
```

