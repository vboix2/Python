# Mòdul math

## Introducció

El mòdul `math` proporciona funcions i constants matemàtiques.
Per importar-lo utilitzarem  la instrucció `import math`.
El llistat d'entitats que conté el podem obtenir fent `dir(math)`:

```
__doc__, __file__, __loader__, __name__, __package__, __spec__, acos, acosh, asin, asinh, atan, atan2, atanh, 
ceil, copysign, cos, cosh, degrees, e, erf, erfc, exp, expm1, fabs, factorial, floor, fmod, frexp, fsum, gamma, 
gcd, hypot, inf, isclose, isfinite, isinf, isnan, ldexp, lgamma, log, log10, log1p, log2, modf, nan, pi, pow, 
radians, sin, sinh, sqrt, tan, tanh, tau, trunc
```

## Constants

* `pi` - nombre pi
* `e` - nombre d'Euler

## Funcions trigonomètriques

* `radians(x)` - converteix un angle x de graus a radians
* `degrees(x)` - converteix un angle x de radians a graus
* `sin(x)` - sinus de x
* `cos(x)` - cosinus de x
* `tan(x)` - tangent de x
* `asin(x)` - arcsinus de x
* `acos(x)` - arccosinus de x
* `atan(x)` - arctangent de x
* `sinh(x)` - sinus hiperbòlic de x
* `cosh(x)` - cosinus hiperbòlic de x
* `tanh(x)` - tangent hiperbòlica de x
* `asinh(x)` - arcsinus hiperbòlic de x
* `acosh(x)` - arccosinus hiperbòlic de x
* `atanh(x)` - arctangent hiperbòlica de x
* `hypot(x, y)` - hipotenusa dels catets x i y

## Funcions exponencials

* `exp(x)` - exponencial de x (e^x)
* `log(x)` - logaritme natural de x 
* `log(x, b)` - logaritme en base b de x 
* `log10(x)` - logaritme en base 10 de x
* `log2(x)` - logaritme binari de x
* `pow(x,y)` - potència y de x (x^y)

## Funcions enteres

* `ceil(x)` - el menor enter més gran o igual a x
* `floor(x)` - el major enter més petit o igual a x
* `trunc(x)` - el valor enter de x, sense decimals
* `factorial(x)` - x!

