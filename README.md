# On floating-point in Swift
Steve Canon (@stephentyrone), July 2016

## Protocols

## Concrete types in the stdlib

## Creating your own FloatingPoint type

## Frequently asked questions (and rejected proposals)
**Q**: Why is `.pi` special?  Why isn't `tau`/`e`/`oneOverPi` also available on `FloatingPoint`?

**A**: There are *lots* of important constants in mathematics.  POSIX defines the following macros:

|Macro|Value|
|-----|-----|
|`M_E` | *e*, the base of the natural logarithm |
|`M_LOG2E` | log2(*e*) |
|`M_LOG10E`| log10(*e*) |
|`M_LN2`| log(2) = 1/log2(*e*) |
|`M_LN10` | log(10) = 1/log10(*e*) |
|`M_PI` | π |
|`M_PI_2` | π/2 |
|`M_PI_4` | π/4 |
|`M_1_PI` | 1/π |
|`M_2_PI` | 2/π |
|`M_2_SQRTPI` | 2/sqrt(π) |
|`M_SQRT2` | sqrt(2) |
|`M_SQRT1_2` | sqrt(1/2) |
