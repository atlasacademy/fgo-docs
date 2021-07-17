### NP Gain

[NP Gain formula](https://blogs.nrvnqsr.com/entry.php/3306-How-much-NP-do-I-get-in-combat)

#### Attacking NP
```
NP% per hit =
(17)    Round Down(
(18)        Round Down(
(19)            offensiveNPRate
(20)            * (firstCardBonus + (cardNpValue * max(1 + cardMod, 0)))
(21)            * enemyServerMod
(22)            * (1 + npChargeRateMod)
(23)            * criticalModifier
            )
(24)        * overkillModifier
        )
```

Mapping of damage formula terms to [buff actions](buff.md):

* cardMod = atkSvt.commandNpAtk - target.commandNpDef
* npChargeRateMod = atkSvt.dropNp

Other constants lookup:

* offensiveNPRate: [NiceServant](https://api.atlasacademy.io/docs#/nice/get_servant_nice__region__servant__item_id__get).noblePhantasms.npGain
* firstCardBonus, cardNpValue:
  * firstCardBonus: [NiceCard](https://api.atlasacademy.io/export/JP/NiceCard.json).card.order.addTdGauge
  * cardNpValue: [NiceCard](https://api.atlasacademy.io/export/JP/NiceCard.json).card.order.adjustTdGauge
* enemyServerMod: sent from server `cache.replaced.battleInfo.userSvt.tdRate`
* criticalModifier: [NiceConstant](https://api.atlasacademy.io/export/JP/NiceConstant.json).CRITICAL_TD_POINT_RATE = 2
* overkillModifier: [NiceConstant](https://api.atlasacademy.io/export/JP/NiceConstant.json).OVER_KILL_NP_RATE = 1.5

#### Defending NP

```
NP% per hit =
        Round Down(
(25)        Round Down(
(26)            defensiveNPRate
(27)            * enemyServerMod
(28)            * (1 + npChargeRateMod)
(29)            * (1 + defensiveChargeRateMod)
            )
            * overkillModifier
        )
```

Mapping of damage formula terms to [buff actions](https://api.atlasacademy.io/export/JP/NiceBuffList.ActionList.json):

* npChargeRateMod = defSvt.dropNp
* defensiveChargeRateMod = defSvt.dropNpDamage

Other constants lookup:
* defensiveNPRate: [NiceServant](https://api.atlasacademy.io/docs#/nice/get_servant_nice__region__servant__item_id__get).npGain.defence
* enemyServerMod: sent from server `cache.replaced.battleInfo.userSvt.tdAttackRate` (Note that this is a different variable from the enemyServerMod in the attacking NP formula above. They are usually the same but they can be different.)
* overkillModifier: [NiceConstant](https://api.atlasacademy.io/export/JP/NiceConstant.json).OVER_KILL_NP_RATE = 1.5
