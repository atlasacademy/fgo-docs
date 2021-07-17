### Floating-point format

If possible, use 32-bit floating-point numbers for calculation in FGO. Here are several examples of how to to do it in several languages:

- C++: https://repl.it/@squaresmile/FGO-NP-gain-in-C
- Python: https://repl.it/@squaresmile/FGO-NP-gain-in-Python
- Javascript:
```js
let f = (v) => Math.fround(v),
    perhit = f(25),
    cardBonus = f(f(1) + f(f(6) * f(f(1) + f(f(800) / f(1000))))),
    finalEnemyMod = f(1),
    gainBonus = f(f(1) + f(300) / f(1000)),
    critBonus = f(2),
    base_gain_no_round = f(f(f(f(perhit * cardBonus) * finalEnemyMod) * gainBonus) * critBonus);

console.log(Math.floor(base_gain_no_round));
console.log(base_gain_no_round);
console.log(cardBonus);
console.log(gainBonus);
```

The expected base NP gain output is 766. If 64-bit floating-point is used, the result will be 767.

If you start the calculation from the numbers the game stores (200, 300, ... which are what the [API](http://api.atlasacademy.io/docs) returns), the boundary between int and float are pretty clear. Buffs' values are summed up in ints and then divided by 1000f when applicable.

#### Test cases
- `!test melt m180 hp10000000 quick crit third af`: 1243 per hit, 4972 total
  - Melt, third quick card, first arts card, 180% quick up + 8% quick up from passive, crit, no overkill hit
- `!test abby m80 hp1 arts crit third ng30 af`: 1149 per hit, 6894 total
  - Abby, third arts card, first arts card, 80% arts up, 30% NP Gain up, crit, all overkill hits
