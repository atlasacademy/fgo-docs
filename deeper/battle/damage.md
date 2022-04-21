### Damage

[Damage formula](https://blogs.nrvnqsr.com/entry.php/3309-How-is-damage-calculated):

```
damage for this card =
(01)    servantAtk
(02)    * npDamageMultiplier
(03)    * {firstCardBonus + [cardDamageValue * max(1 + cardMod, 0)]}
(04)    * classAtkBonus
(05)    * triangleModifier
(06)    * attributeModifier
(07)    * randomModifier
(08)    * 0.23
(09)    * max(1 + atkMod - defMod, 0)
(10)    * criticalModifier
(11)    * extraCardModifier
(12)    * max(1 - specialDefMod, 0)
(13)    * max([1 + powerMod + selfDamageMod + (critDamageMod * isCrit) + (npDamageMod * isNP)], 0.001)
(18)    * max(1 + damageSpecialMod, 0.001)
(14)    * [1 + ((superEffectiveModifier - 1) * isSuperEffective)]
(15)    + dmgPlusAdd
(16)    + selfDmgCutAdd
(17)    + (servantAtk * busterChainMod)

damage = Math.Floor(Math.Max(damage, 0))
```

Mapping of damage formula terms to [buff actions](buff.md):

* cardMod = actor.commandAtk - target.commandDef
* atkMod = actor.atk
* defMod = target.defence or target.defencePierce if it's a defence piercing NP
* specialDefMod = target.specialdefence
* powerMod = actor.damage + actor.damageIndividuality + actor.damageIndividualityActiveonly + actor.damageEventPoint
* selfDamageMod = target.selfdamage
* critDamageMod = actor.criticalDamage
* npDamageMod = actor.npdamage
* damageSpecialMod = actor.damageSpecial
* superEffectiveModifier = function Correction value
* dmgPlusAdd = actor.givenDamage
* selfDmgCutAdd = target.receiveDamage

Other constants lookup:

* npDamageMultiplier: only applies to NP card, 1 otherwise
* firstCardBonus, cardDamageValue:
  * firstCardBonus: [NiceCard](https://api.atlasacademy.io/export/JP/NiceCard.json).card.order.addAtk
  * cardDamageValue: [NiceCard](https://api.atlasacademy.io/export/JP/NiceCard.json).card.order.adjustAtk
* classAtkBonus: [NiceClassAttackRate](https://api.atlasacademy.io/export/JP/NiceClassAttackRate.json).class
* triangleModifier: [NiceClassRelation](https://api.atlasacademy.io/export/JP/NiceClassRelation.json).actor.target
* attributeModifier: [NiceAttributeRelation](https://api.atlasacademy.io/export/JP/NiceAttributeRelation.json).actor.target
* criticalModifier: [NiceConstant](https://api.atlasacademy.io/export/JP/NiceConstant.json).CRITICAL_ATTACK_RATE = 2 (only applies if critical, 1 otherwise)
* busterChainModifier: [NiceConstant](https://api.atlasacademy.io/export/JP/NiceConstant.json).CHAINBONUS_BUSTER_RATE = 0.2 if buster card in buster chain, 0 otherwise
* extraCardModifier:
  * [NiceConstant](https://api.atlasacademy.io/export/JP/NiceConstant.json).EXTRA_ATTACK_RATE_GRAND = 3.5 if it's a color brave chain
  * [NiceConstant](https://api.atlasacademy.io/export/JP/NiceConstant.json).EXTRA_ATTACK_RATE_SINGLE = 2 otherwise
  * 1 if not extra card
