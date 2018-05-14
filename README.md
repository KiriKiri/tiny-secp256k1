# tiny-secp256k1

## isPoint (A) -> bool
``` haskell
isPoint :: Buffer -> bool
```
Returns `false` if
* `A` is not encoded with a sequence tag of `0x02`, `0x03` or `0x04`
* `A.x` is not in `[1...p - 1]`
* `A.y` is not in `[1...p - 1]`

## isPointCompressed (A) -> bool
``` haskell
isPointCompressed :: Buffer -> bool
```
Returns `false` if the signature is **not** compressed.

## isPrivate (d) -> bool
``` haskell
isPrivate :: Buffer -> bool
```
Returns `false` if
* `d` is not 256-bit, or
* `d` is not in `[1..order - 1]`

## pointAdd (A, B[, compressed]) -> ?Buffer
``` haskell
pointAdd :: Buffer -> Buffer [-> bool] -> Maybe Buffer
```
Returns `null` if result is at infinity.

##### Throws:
* `Expected Point` if `!isPoint(A)`
* `Expected Point` if `!isPoint(B)`

## pointAddScalar (A, tweak[, compressed]) -> ?Buffer
``` haskell
pointAddScalar :: Buffer -> Buffer [-> bool] -> Maybe Buffer
```
Returns `null` if result is at infinity.

##### Throws:
* `Expected Point` if `!isPoint(A)`
* `Expected Tweak` if `tweak` is not in `[0...order - 1]`

## pointCompress (A, compressed) -> Buffer
``` haskell
pointCompress :: Buffer -> bool -> Buffer
```

##### Throws:
* `Expected Point` if `!isPoint(A)`

## pointFromScalar (d[, compressed]) -> ?Buffer
``` haskell
pointFromScalar :: Buffer [-> bool] -> Maybe Buffer
```
Returns `null` if result is at infinity.

##### Throws:
* `Expected Private` if `!isPrivate(d)`

## privateAdd (d, tweak) -> ?Buffer
``` haskell
privateAdd :: Buffer -> Buffer -> Maybe Buffer
```
Returns `null` if result is equal to `0`.

##### Throws:
* `Expected Private` if `!isPrivate(d)`
* `Expected Tweak` if `tweak` is not in `[0...order - 1]`


## sign (h, d) -> Buffer
``` haskell
sign :: Buffer -> Buffer -> Buffer
```

##### Throws:
* `Expected Private` if `!isPrivate(d)`
* `Expected Scalar` if `h` is not 256-bit

## verify (h, Q, signature[, strict = false]) -> bool
``` haskell
verify :: Buffer -> Buffer -> Buffer -> bool
```
Returns `false` if any of (r, s) values are equal to `0`,  or if the signature is rejected.

If `strict` is `true`, valid signatures with any of (r, s) values greater than `n / 2` are rejected.

##### Throws:
* `Expected Point` if `!isPoint(Q)`
* `Expected Signature` if `signature` has any (r, s) values not in range `[0...order - 1]`
* `Expected Scalar` if `h` is not 256-bit
