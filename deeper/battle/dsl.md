<div style="text-align:center"><img src="../../images/use_big_sl.png"></div>

## Big SL and Deep SL
This page will discuss other SL methods that give players a lot more chances to get good RNG rolls compared to mormal SL.

### Motivation
Some TA scripts require a lot of favorable and unlikely RNG rolls to succeed. To change the outcome of a particular RNG roll, you can close the game and [advance the RNG state](../../README.md#what-affects-whether-a-card-procs-critical-hit) to get a different RNG roll. I will refer to this method as normal SL.

However, normal SL has some major drawbacks. Firstly, you can only return to the state right before the RNG advancing action is taken. Secondly, you are limited to a short list of RNG advancing actions possible and if you run out of them, you will have to restart the quest. Big and Deep SL are a way to overcome these limitations.

Note that both Big and Deep SL work on the unmodified game client.

### Background
- The game uses the [Random](https://docs.microsoft.com/en-us/dotnet/api/system.random?view=netframework-4.6) C# class for the RNG calculations.
- The game gets [the RNG seed](https://docs.microsoft.com/en-us/dotnet/api/system.random.-ctor?view=netframework-4.6#system-random-ctor(system-int32)) from the server and uses it to initialize the RNG. The server will return the same seed when the player resumes the quest on the same device.
- The game saves the battle state in a save file stored on the device. That's why if you are [logged in on multiple devices](https://www.reddit.com/r/grandorder/comments/hfbz0h/fgo_save_files_for_na_and_jp_play_on_multiple/), you can start the quest on one device but can't resume the quest on another device at the same battle state.
- The battle state is saved after major actions including but not limited to end of turn and skill use. That's why you need to close the game before those actions finish to do normal SL.
- In order to restore the RNG state, the number of times the RNG has been advanced is stored in the save file. When the player resumes the quest, the game initializes the RNG using the seed from the server and [advances the RNG](https://docs.microsoft.com/en-us/dotnet/api/system.random.next?view=netframework-4.6#system-random-next) for the same number of times.
- Besides the number of RNG advances, the battle state save file also stores all parameters of field entities including ATK, HP, skill cooldowns, active buffs, ...

### Big SL
Big SL refers to the act of making copies of the battle state save file at different points in time and restoring them later. This allows one to return to any earlier save point instead of being limited to the moment before the latest RNG changing action. After returing to an earlier save point, one is free to try different RNG advancing actions to get different outcomes.

Some actions, such as command spell usage, are not saved in the save file but sent to the server so they can't be restored using an earlier save file.

### Deep SL
Deep SL goes further and edits the battle save file directly. One can edit the number of RNG advances in the save file, repackage it and resume the quest with a new RNG roll without using any in game action. Combining with big SL, this allows one a lot of  freedom to try as many RNG rolls as possible.

Note that with an unmodified client, Deep SL can only manipulate the number of RNG advances but not the RNG seed that comes from the server. There's no guarantee that a different number of RNG advances will be favorable. One would still need to check the game client to see if the RNG rolls succeeds.

If one can record the RNG seed, either from dumping the memory or looking at the traffic, one can replicate the RNG state on another device without having to use the game client. After that, they can simply run as many RNG rolls as possible to look for a favorable number of RNG advances and edit the save file accordingly.

It's also possible to edit other variables in the battle state save file. For example, one can increase the servant's attack or attack buff value to get higher damage.
