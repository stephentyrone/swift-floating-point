# On floating-point in Swift
Steve Canon (@stephentyrone), July 2016

## Frequently asked questions
**Q**: Why is `.pi` special?  Why isn't `tau`/`e`/`oneOverPi` also available on `FloatingPoint`?

**A**: There are *lots* of important constants in mathematics.  POSIX defines the following macros in C:

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

It would certainly be possible to add all of these and more as static properties on the `FloatingPoint` protocol.  However, there is a big drawback to this approach to keep in mind.  The C macros are in the global namespace and don't pollute autocomplete lists; static properties on protocols appear in the autocomplete list when you write `Float.<TAB>`.  That list is already pretty large for floating point types; adding 12 or more new values with short, cryptic names would only add noise.

So why is `.pi` included?  We talked about this when [SE-0067](https://github.com/apple/swift-evolution/blob/master/proposals/0067-floating-point-protocols.md) was proposed; it turns out that in real code, `M_PI` and its variants like `M_PI_2` are used about an order of magnitude more frequently than all other constants combined.  So it makes sense to carve out an exception for `.pi`.  If you want `M_PI_2`, just write `(Float.pi / 2)`, which is always computed exactly for binary floating-point types, so you're not losing any accuracy.

All of this isn't to say that an expanded set of constants won't be available in the future; they're simply unlikely to be approved as top-level members of the `FloatingPoint` protocol.  I can definitely imagine everyone agreeing to `Float.Constant.e`, for example.
