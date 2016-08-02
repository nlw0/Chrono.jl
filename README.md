# Chrono

*Scientific timekeeping  in Julia*

[![Build Status](https://travis-ci.org/andyferris/Chrono.jl.svg?branch=master)](https://travis-ci.org/andyferris/Chrono.jl)

[![Coverage Status](https://coveralls.io/repos/andyferris/Chrono.jl/badge.svg?branch=master&service=github)](https://coveralls.io/github/andyferris/Chrono.jl?branch=master)

[![codecov.io](http://codecov.io/github/andyferris/Chrono.jl/coverage.svg?branch=master)](http://codecov.io/github/andyferris/Chrono.jl?branch=master)

This package provides a flexibile interface to write `Duration`s of time, and to
functionality to keep track of instants of `Time` relative to specified
`Clock`s. The design is partially motivated by *C++*'s `std::chrono` template
library.

Current functionality includes storage of `Duration`s using any number type
and in periods of any chosen fraction of a second, a smattering of `Clock`s
based on the *International Atomic Time* (TAI) standard such as *UTC* and
*GPS* time standards. The `Time` type wraps a `Duration` since the start time
(a.k.a. *epoch*) of a `Clock`.

### Quick start
```julia
julia> using Chrono

julia> t1 = Time(12hours + 3.0seconds, UTCDate(2016,7,25))
43203.0 seconds (since 2016-07-25 (UTC))

julia> t2 = Time(14hours + 2minutes + 1.0seconds, UTCDate(2016,8,2))
50521.0 seconds (since 2016-08-02 (UTC))

julia> t2 - t1
698518.0 seconds

julia> t3 = Time(5hours + 5minutes + 26.0nanoseconds, GPSWeek(2016,1,1))
1.8300000000026e13 nanoseconds (since GPS week 1877 (2015-12-27))

julia> t4 = Time(t3, UTCDate(2015,12,27))
1.8317000000026e13 nanoseconds (since 2015-12-27 (UTC))

julia> t3.duration - t4.duration
-1.7e10 nanoseconds

julia> t3.clock - t4.clock
17//1 seconds
```
