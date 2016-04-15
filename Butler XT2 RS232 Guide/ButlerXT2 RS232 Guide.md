#Butler XT2 RS-232 interface

The Butler XT2 supports control via RS-232. With the right information it is a fairly straightforward protocol to use. The RS-232 protocol allows for access to the following features:

##Physical Connection
![Connection Illustration](http://ruby-lighting.com/github/ecue-technical-documents/Butler-XT2-RS232-Terminal-Illustration.jpg)

##Connection Settings
|Parameter	|Setting|
|---------	|-------|
|Baud		| 9600
|Bits		|8
|Parity		|None
|Stop Bit	|1


##Protocol Details
The protocol is fairly simple and contains only a few commands. All commands have the following aspecs in common: 
- Each command starts with a two-letter command code
- Each command has one or two 3-digit prameter with [leading 0's](https://en.wikipedia.org/wiki/Leading_zero)
- All commands must be followed by a newline and a carrage return (`\r\n` or `\0x0d \0x0a`) to be recognized by the buttler


|Command Code	|Parameters			|Action					|Example
|---------------|-------------------|-----------------------|--------------
|PC				| 1 - Cuelist Index	| Play cuelist			| Play cuelist 5: `PC005\r\n`
|TP				| 1 - Cuelist Index	| Toggle cuelist on/off | Toggle cuelist 3: `TP003\r\n`
|PP				| 1 - Cuelist Index | Toggle cuelist play/pause| Toggle cuelist 35 pause: `PP035\r\n`
|NX				| 1 - Mutex Group Index| Play the next cuelist in a *mutex group*^1^| Play next cue in *mutex group* 3: `NX003\r\n`
|PX				| 1 - Mutex Group Index| Play the previous cuelist in a *mutex group*<sup>1</sup>| Play previous cue in *mutex group* 75: `NX075\r\n`
|IN				| 1 - Fader Index <br>`0 = Grandmaster` <br>` 1-99 = Cuelist Master` <br>`129-193 = Versatile master`<br><br>2 - Level (0-100) | Set the level of a fader. <br><br> Versatile masters 1-64 are mapped to indicies 129-193.	| Grandmaster to 50%: `IN000050\r\n` <br><br>Cuelist submaster 5 to 80%: `IN005080\r\n`<br><br> Versatile master 3 to 100%: `IN131100\r\n`
|ST				| 1 - Cuelist Index	|Stop cuelist. <br><br>If the index is 0, all cuelists will be stopped. | Stop All Cuelists: `ST000\r\n`<br><br>Stop cuelist 22: `ST022\r\n`
<sup>[1]</sup> A mutexgroup is a group of cuelists from which only one cuelist can play at any given time. If one cuelist in the group is playing and another is started, the original cuelist is stopped automatically and the new cuelist plays.

