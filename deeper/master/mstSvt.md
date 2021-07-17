## File : `mstSvt.json`
This file holds Servants' (including the unplayables) and Craft Essences' data. Mostly.

A Servant object would look like this :
```json
{
    "relateQuestIds": [91600501],
    "individuality": [5000, 600500, 2, 105, 201, 301, 304, 1000, 2001, 2008, 2011, 2037],
    "classPassive": [50551],
    "cardIds": [3, 3, 3, 1, 2],
    "script": {},
    "id": 600500,
    "baseSvtId": 600500,
    "name": "Jack the Ripper",
    "ruby": "Jack the Ripper",
    "battleName": "Jack",
    "classId": 6,
    "type": 1,
    "limitMax": 4,
    "rewardLv": 90,
    "friendshipId": 1049,
    "maxFriendshipRank": 10,
    "genderType": 2,
    "attri": 3,
    "combineSkillId": 600500,
    "combineLimitId": 600500,
    "sellQp": 5000,
    "sellMana": 9,
    "sellRarePri": 5,
    "expType": 25,
    "combineMaterialId": 5,
    "cost": 16,
    "battleSize": 2,
    "hpGaugeY": -250,
    "starRate": 255,
    "deathRate": 440,
    "attackAttri": 1,
    "illustratorId": 12,
    "cvId": 10,
    "collectionNo": 75,
    "materialStoryPriority": 1000
}
```

I'll go through each line.

- `relateQuestIds` : Quests relating to this Servant. Their IDs are defined here.
  The respective quests seem to be defined in `mstQuest.json`:
  ```json
  {
    "afterActionVals": [],
    "id": 91600501,
    "name": "Jack Kills Jack",
    "nameRuby": "",
    "type": 3,
    "consumeType": 1,
    "actConsume": 20,
    "chaldeaGateCategory": 0,
    "spotId": 10402,
    "giftId": 0,
    "priority": 639949,
    "bannerType": 0,
    "bannerId": 0,
    "iconId": 0,
    "charaIconId": 6005000,
    "giftIconId": 8,
    "forceOperation": 0,
    "afterClear": 1,
    "displayHours": 0,
    "intervalHours": 0,
    "chapterId": 1,
    "chapterSubId": 1,
    "chapterSubStr": "",
    "recommendLv": "70",
    "hasStartAction": 1,
    "flag": 0,
    "scriptQuestId": 0,
    "noticeAt": 946684800,
    "openedAt": 946684800,
    "closedAt": 1893456000
  }
  ```
- `individuality` : Traits. This actually maps to certain functions in the game code.
  For example, `2008` seems to stand for Servants without the Star attribute (which means immunity to Enuma Elish's Special Attack)
- `classPassive` : Passive skills. IDs of skill objects defined in `mstSkill.json`, with respective details in `mstSkillDetail.json`.
  In this case, `50551` stands for Presence Concealment :
  - `mstSkill.json`:
    ```json
    {
        "effectList": [],
        "actIndividuality": [],
        "script": {},
        "id": 50551,
        "type": 2,
        "name": "Presence Concealment A+",
        "ruby": "Presence Concealment ",
        "maxLv": 10,
        "iconId": 105,
        "motion": 101
    }
    ```
  - `mstSkillDetail.json`:
    ```json
    {
        "id": 50551,
        "detail": "Increase your C. Star Drop Rate",
        "detailShort": "Increase your C. Star Drop Rate"
    }
    ```
- `cardIds` : Card set. Consult the following TypeScript line:
  ```ts
  enum CardType { ARTS = 1 as 1, BUSTER = 2 as 2, QUICK = 3 as 3 };
  ```
- `script` : Unknown to me at the time I write this, probably be added when I know more details.
- `id`, `baseSvtId` : Internal (I mean, really internal) game ID of this servant.
  The game refers to servants with this ID, not the ID you see in **Spirit Origin List**.
  The first two digits define the class. The meaning is as follows :
  ```ts
  enum ClassType {
    Saber = 1 as 1,
    Archer = 2 as 2,
    Lancer = 3 as 3,
    Rider = 4 as 4,
    Caster = 5 as 5,
    Assassin = 6 as 6,
    Berserker = 7 as 7,
    Shielder = 8 as 8,
    Ruler = 9 as 9,
    AlterEgo = 10 as 10,
    Avenger = 11 as 11,
    MoonCancer = 23 as 23,
    Foreigner = 25 as 25
  }
  ```
  The next two digits are unique for every Servant in the same class. See [here](http://blogs.nrvnqsr.com/entry.php/3471-Internal-Servant-s).
  Not sure about the last two digits though.
- `name`, `ruby` : Self-explanatory. If you don't know what is `ruby`, see [this Wikipedia article](https://en.wikipedia.org/wiki/Ruby_character).
- `battleName` The name you see during battle, under the HP and NP bar.
- `classId` : Class ID. See above.
- `type` : Defines the object type. If you know C# enums, you will know which (numeral) values correspond to which type.
  ```cs
  public enum Type
    {
		NORMAL = 1,
		HEROINE,
		COMBINE_MATERIAL,
		ENEMY,
		ENEMY_COLLECTION,
		SERVANT_EQUIP,
		STATUS_UP,
		SVT_EQUIP_MATERIAL,
		ENEMY_COLLECTION_DETAIL,
		ALL,
		COMMAND_CODE
	}
  ```
  - `1` is definitely a normal Servant.
  - `4` is an enemy, surely. It is even hardcoded :
    ```cs
    public static bool IsEnemy(int type)
	{
		return type == 4;
	}
    ```
  - `6` seems to define Craft Essences. Proven here :
    ```json
    {
      "relateQuestIds": [],
      "individuality": [],
      "classPassive": [],
      "cardIds": [3, 3, 3, 3, 3],
      "script": {},
      "id": 9400340,
      "baseSvtId": 9400340,
      "name": "Kaleidoscope",
      "ruby": "Kaleidoscope",
      "battleName": "-",
      "classId": 1001,
      "type": 6
    }
    ```
    Didn't figure out other types, maybe I will when time allows.
- `limitMax` : Not sure what for.
  > `limitMax` is usually found when drawing servants and equips
  
  _Cereal#5579_
- `rewardLv` : Doesn't seem to be used for anything. Maybe max level without grails?
- `friendshipId` : Bond set ID. See `mstFriendship.json`.
  ```json
  [{
    "id": 1049,
    "rank": 0,
    "friendship": 5000
  }, {
    "id": 1049,
    "rank": 1,
    "friendship": 20000
  }, {
    "id": 1049,
    "rank": 2,
    "friendship": 30000
  }, {
    "id": 1049,
    "rank": 3,
    "friendship": 32000
  }, {
    "id": 1049,
    "rank": 4,
    "friendship": 50000
  }, {
    "id": 1049,
    "rank": 5,
    "friendship": 200000
  }, {
    "id": 1049,
    "rank": 6,
    "friendship": 630000
  }, {
    "id": 1049,
    "rank": 7,
    "friendship": 970000
  }, {
    "id": 1049,
    "rank": 8,
    "friendship": 1290000
  }, {
    "id": 1049,
    "rank": 9,
    "friendship": 1695000
  }, {
    "id": 1049,
    "rank": 10,
    "friendship": -1
  }]
  ```
  These are the bond amounts required each level for Jack. Note the `-1` at the end, seems to be infinity - you can't go past bond 10 (unless you're on JP, I'm documenting NA).
- `maxFriendshipRank` : maximum bond levels. Seems to be 10 for servants, 0 for anything else.
- `genderType` : Gender. `2` is Female. `1` is Male. `3` is... well, Astolfo has it.
  My theory is that these values are bitmasks and ANDed each other, representing Astolfo "having" both genders.

To be continued...