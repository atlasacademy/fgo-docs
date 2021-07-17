## File : `mstSvtTreasureDevice.json`
This file holds a pivot object linking servants and noble phantasms(treasure device).

```json
{
    "damage":[10,20,30,40],
    "strengthStatus":2,
    "svtId":600500,
    "num":1,
    "priority":102,
    "flag":0,
    "imageIndex":0,
    "treasureDeviceId":600502,
    "condQuestId":91600501,
    "condQuestPhase":3,
    "condLv":0,
    "condFriendshipRank":0,
    "motion":50,
    "cardId":3
}
```

Breakdown:

- `damage` : Damage distribution. `damage.length` = number of hits. Each hit is `(damage[i]/sum(damage)) * np_damage`. Note: due to some data entry issues, there is a possibility of the sum of `damage` to not equal 100. In such cases, the total damage of the NP can be over 100% of the np_damage.
- `strengthStatus` : Unknown
- `svtId` : Servant id. See `mstSvt.json`
- `num` : Unknown
- `priority` : Servants can have multiple noble phantasms they have unlocked due to interludes, rank ups, story missions, etc. In such cases, the noble phantasm applied (unless set otherwise) is the noble phantasm with the highest priority. Cases otherwise include enemy servants with Extra attack as noble phantasms instead of their default one.
- `flag` : Unknown
- `imageIndex` : Unknown
- `treasureDeviceId` : Noble Phantasm id. See `mstTreasureDevice.json`
- `condQuestId` : Quest required to unlock this noble phantasm. Interludes and rank up quests can be identified by the id. `91######` = Interlude. `94######` = Rank Up. See `mstQuest.json`
- `condQuestPhase` : Arrow for quest required to unlock noble phantasm. The specific arrow can be identified by `mstQuestPhase.json`
- `condLv` : Unknown. Implies level required for unlock but no entires have non-zero values.
- `condFriendshipRank` : Unknown. Implies bond required for unlock but no entries have non-zero values.
- `motion` : Unknown
- `cardId` : Card type. See following enum:
  ```ts
  enum CardType { ARTS = 1 as 1, BUSTER = 2 as 2, QUICK = 3 as 3 };
  ```
