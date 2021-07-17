Buff actions values are calculated using the following formula:
```python
num = buffAction.baseParam + (total plusTypes buffs values) - (total minusTypes buff values)

if buffAction.limit in (normal, lower):
    if num < 0:
        num = 0

num = num - buffAction.baseValue;

if buffAction.limit in (normal, upper):
    if maxRate < num:
        num = maxRate

return num
```

- Buff action variables can be found [here](https://api.atlasacademy.io/export/JP/NiceBuffList.ActionList.json):
- `baseParam`
- `baseValue`
- `limit`
- `maxRate` is a property of the buff item. This value can be found in the [DB](https://apps.atlasacademy.io/db/#/) or [API](https://api.atlasacademy.io/docs). If there are multiple buffs, the last `maxRate` is used. Different buffs of the same buff action usually have the same `maxRate` value.
- For example: we are trying to calculate `cardMod` with 10 level 10 Merlin's [Hero Creation](https://apps.atlasacademy.io/db/#/NA/skill/323650) applied and no buster damage down:
- `cardMod` -> buff action `commandAtk` -> `plusTypes` [buff type](https://apps.atlasacademy.io/db/#/NA/buff/102) `upCommandall`
    - `baseParam`: 1000
    - `baseValue`: 0
    - `limit`: normal
    - `maxRate`: 5000
- `num` = 1000 + 500 * 10 = 6000 (`baseParam` = 1000 and there are 10 Hero Creation, each has `Value` of 500)
- `limit` is normal but `num` > 0 so lower bound is not applied
- `num` = `num` - `baseValue` = 6000 - 0 = 6000
- `limit` is normal and `num` > `maxRate` so upper bound is applied -> `num` = 5000
- The final `cardMod` value is 5000 or 500%.
