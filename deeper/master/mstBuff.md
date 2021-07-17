## File : `mstBuff.json`
This file holds buff objects.

```json
{
    "vals": [3004, 3007, 3040],
    "tvals": [],
    "individualities": [],
    "ckOpIndv": [],
    "script": {},
    "id": 218,
    "buffGroup": 0,
    "type": 74,
    "name": "Death Resist Up",
    "detail": "Increase Death resistance",
    "iconId": 306,
    "maxRate": 5000
}
```

Breakdown:

- `vals`: list of individualities
- `tvals`: list of target individualities
- `ckOpIndv`:
- `script`:
- `id`: buff id
- `buffGroup`:
- `type`: buff type, maps to `BuffList.TYPE`, used to map to buff action
- `name`: buff name
- `detail`: more detailed name of buff
- `iconId`:
- `maxRate`: used to calculate the maximum value of buff action. The effective max of additional buff is `maxRate + baseValue - baseParam`. Default value of `baseValue` is 0 and of `baseParam` is 1000. `baseValue` and `baseParam` are set when the corresponding `BuffList.ActInfo` is created.
