## File : `mstSkillLv.json`
This file holds servants' skills level details.

```json
{
    "funcId": [358, 338, 470],
    "svals": ["[5000,1,-1,2600]", "[1000,1,-1,3600]", "[1000,1]"],
    "script": {},
    "skillId": 133000,
    "lv": 9,
    "chargeTurn": 7,
    "skillDetailId": 133000,
    "priority": 0
}
```

Breakdown:

- `funcId`: list of functions id: `mstFunc.id`.
- `svals`: list of values passed to the function objects. DataVals will process this list differently depending on function's types. Check out the DataVals class for specifics.
- `script`:
- `skillId`: `id` in `mstSkill`
- `lv`: level of the skill
- `chargeTurn`: skill cooldown
- `skillDetailId`: `id` in `mstSkillDetail`
- `priority`:
