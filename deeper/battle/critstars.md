### Crit stars

[Crit stars formula](https://blogs.nrvnqsr.com/entry.php/3307-How-many-crit-stars-do-I-get-in-combat)

```
dropChancePerHit =
        (
(30)      baseStarRate
(31)      + firstCardBonus + (cardStarValue * max(1 + cardMod, 0))
(32)      + serverRate
(33)      + starDropMod
(34)      - enemyStarDropMod
(35)      + criticalModifier
        )
(36)    * overkillModifier
(37)    + overkillAdd
```

Mapping of damage formula terms to [buff actions](buff.md):

* cardMod = atkSvt.commandStarAtk - defSvt.commandStarDef
* starDropMod = atkSvt.criticalPoint
* enemyStarDropMod = defSvt.criticalPoint

Other constants lookup:

* baseStarRate: [NiceServant](https://api.atlasacademy.io/docs#/nice/get_servant_nice__region__servant__item_id__get).starGen
* firstCardBonus, cardStarValue:
  * firstCardBonus: [NiceCard](https://api.atlasacademy.io/export/JP/NiceCard.json).card.order.addCritical
  * cardStarValue: [NiceCard](https://api.atlasacademy.io/export/JP/NiceCard.json).card.order.adjustCritical
* serverRate: sent from server `cache.replaced.battleInfo.userSvt.starRate`
* criticalModifier: [NiceConstant](https://api.atlasacademy.io/export/JP/NiceConstant.json).CRITICAL_STAR_RATE = 0.2
* overkillModifier: [NiceConstant](https://api.atlasacademy.io/export/JP/NiceConstant.json).OVER_KILL_STAR_RATE = 1
* overkillAdd: [NiceConstant](https://api.atlasacademy.io/export/JP/NiceConstant.json).OVER_KILL_STAR_ADD = 0.3