# Polyline Encoder/Decoder
C++ implementation of [Google Encoded Polyline Algorithm Format.](https://developers.google.com/maps/documentation/utilities/polylinealgorithm)<br>
The implementation guarantees to conform with the results of the [Google Interactive Polyline Encoder Utility.](https://developers.google.com/maps/documentation/utilities/polylineutility)

[![Build Status](https://travis-ci.org/vahancho/polylineencoder.svg?branch=master)](https://travis-ci.org/vahancho/polylineencoder)
[![Build status](https://ci.appveyor.com/api/projects/status/6tg1kkp5fgk3x2fd?svg=true)](https://ci.appveyor.com/project/vahancho/polylineencoder)
[![Coverage Status](https://coveralls.io/repos/github/vahancho/polylineencoder/badge.svg?branch=master)](https://coveralls.io/github/vahancho/polylineencoder?branch=master)
[![codecov](https://codecov.io/gh/vahancho/polylineencoder/branch/master/graph/badge.svg)](https://codecov.io/gh/vahancho/polylineencoder)

## Installation

No installation required. Just compile *polylineencoder.h(.cpp)* in your project and use `gepaf::PolylineEncoder` class.

## Prerequisites

No special requirements except *C++11* compliant compiler. The class is tested with *gcc 4.8.4* and *MSVC 12.0* (Visual Studio 2013).
For more details see the CI badges (*Travis CI & AppVeyor CI*).

## Usage Example:

All code is in `gepaf` namespace. `gepaf` stands for *Google Encoded Polyline Algorithm Format*.

```cpp
gepaf::PolylineEncoder encoder;

// Poles and equator.
encoder.addPoint(-90.0, -180.0);
encoder.addPoint(.0, .0);
encoder.addPoint(90.0, 180.0);

auto res = encoder.encode(); // "~bidP~fsia@_cidP_gsia@_cidP_gsia@"
encoder.clear(); // Clear the list of points.

// Decode a string using static function.
auto polyline = gepaf::PolylineEncoder::decode("~bidP~fsia@_cidP_gsia@_cidP_gsia@");

// Iterate over all points and print coordinates of each.
for (const auto &point : polyline) {
    printf("(%f, %f)\n", point.latitude(), point.longitude());
}
```

## Test

There are unit tests provided for `PolylineEncoder` class. You can find them in the *test/* directory.
To run them you have to build and run the test application. For doing that you must invoke the following
commands from the terminal, assuming that compiler and environment are already configured:

##### Linux (gcc)
```
cd test
g++ -std=c++11 main.cpp -o test
./test
```

##### Windows
```
cd test
cl /W4 /EHsc main.cpp /link /out:test.exe
test
```

## See Also

* [Encoded Polyline Algorithm](https://developers.google.com/maps/documentation/utilities/polylinealgorithm)

