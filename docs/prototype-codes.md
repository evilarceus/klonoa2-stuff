# Prototype Build Cheat Codes + Memory Addresses
More info: [Klonoa 2: Lunatea's Veil (Jun 4, 2001 Prototype) - Hidden Palace](https://hiddenpalace.org/Klonoa_2:_Lunatea%27s_Veil_(Jun_4,_2001_prototype))
* According to the string at `003610B0` and `003610C0`, the real build date might be around `Dec 13 2000 16:27:35`.

Sections
* [Debug Stuff](https://github.com/evilarceus/klonoa2-stuff/blob/main/docs/prototype-codes.md#debug-stuff)
* [Klonoa/Camera](https://github.com/evilarceus/klonoa2-stuff/blob/main/docs/prototype-codes.md#klonoacamera)

## Debug Stuff
### .pnach file
Name this file `3F81E474.pnach` and put it in the `cheats` directory of PCSX2 to use all the codes below.
```
gametitle=Klonoa 2 Prototype
patch=1,EE,D034FC82,extended,0000FFFD
patch=1,EE,20303F38,extended,00000001
patch=1,EE,202D0C60,extended,080B7158
patch=1,EE,20179FF0,extended,00000000
```

### Debug Menu
This build includes a debug menu, which can be accessed by writing `0x1` to the address `00303F38`. Credit to [punk7890](https://twitter.com/punk_7890/status/1206743316995297280) for finding the menu and creating the code: "Most [options] don't work since it requires files from the developer's computer. Level select and sound tests do work."

The following code will activate the debug menu when you press L3.
```
D034FC82 0000FFFD
20303F38 00000001
```
### Debug Logging
The game will print `hInitBoot ...` when you boot up the game, but will stop printing after the game initializes. This code redirects `printf` calls to use `scePrintf` instead.
```
202D0C60 080B7158
```
Example output:
```
hSndBankSetStage ... done
hInitStage0 ... done
hInitStage0(); ok
kzStageInit0(); ok
nkStageInit0(); ok
FileRead0 count = 0
GameDataTop=00c32000 mode=1
hCdRead LSN=51844 nSEC=7026 BUFF=00c32000
hInitStage1 ...
hEvStageInit ...
tblmax=4
tblmax=4
hInitStage1 ... done
NakanoPackAdr = c32030
hrData 18c3940 4 ==== Read
hrData 18c3960 1980ca0 ==== OK
areatop 0xc5c800 current 0x19f1220
buffareatop seted 0x19f1220
area memory format.
program buffer memory reports. (0x100h block) 2/4096 used.
program buffer memory reports. (0x400h block) 1/1024 used.
program buffer memory reports. (0x2000h block) 1/64 used.
area memory end.
初期化
dst:0x1cf1220  radr:0x1d39e30
start x:0  y:0  z:0
grid  x:33  y:7  z:28
grid  w:128  h:256  
=============================================

 Decode = 501648
Read config file
BG GMS 1980ce0 === ok
VPA GMS 19951b0 === dummy
VPO GMS 19951c0 === dummy
Pack == DecodeBg 0
Pack == DecodeBg 1
Pack == DecodeBg 2
Pack == Get BG_ANM 1
Pack == VPA Dummy !!
Pack == VPO Dummy !!
Pack == MiniPuppet Dummy !!
Pack == Puppet
No VPA Data
movie type = VT
movie bsDataSize = 738464
movie nframes = 60
movie texbp = 13568 0x3500
movie thVal0 = 0 thVal1 = 0
movie incnum = 2
movie width = 128
movie height = 128
movie mbx = 8
movie mby = 8
movie texbw = 2
movie tw = 7
movie th = 7
hGameAreaStart ...
hEvAreaInit ... 0100
hEvAreaInit ... done
hSeEnvStart ...
hSeEnvStart ... done
hGameAreaStart ... done
Init Area OK!!
hPushRestart ...
EVOL=-0.0e+1
BGM =0
hPushRestart ... done
nakano > Obj Klonoa Init
```

### Disable Idle Timer
This code will prevent the game from going back to the main menu when you do not input a control after 30 seconds. Note that the idle timer on the menu will stay active.
```
20179FF0 00000000
```

## Klonoa/Camera
| Region    | Address  |
|-----------|----------|
| Prototype | 002FC060 |

| Address    | Description                     |
|------------|---------------------------------|
| ADDR+0x00  | Camera Position X               |
| ADDR+0x04  | Camera Position Y               |
| ADDR+0x08  | Camera Position Z               |
| ADDR+0x14  | Camera Rotation (-3.14 to 3.14) |
| ADDR+0x60  | Klonoa [State](https://github.com/evilarceus/klonoa2-stuff#state) (byte)             |
| ADDR+0x70  | Klonoa Position X               |
| ADDR+0x74  | Klonoa Position Y               |
| ADDR+0x78  | Klonoa Position Z               |
| ADDR+0x80  | Klonoa Speed X                  |
| ADDR+0x84  | Klonoa Speed Y                  |
| ADDR+0x88  | Klonoa Speed Z                  |
| ADDR+0x1B0 | Klonoa Rotation X (Unused)      |
| ADDR+0x1B4 | Klonoa Rotation Y (Unused)      |
| ADDR+0x1B8 | Klonoa Rotation Z (Unused)      |

### State
| Hex (Decimal) | State                                 |
|---------------|---------------------------------------|
| 00 (0)        | None                                  |
| 01 (1)        | Walking                               |
| 02 (2)        | Jumping/Falling                       |
| 03 (3)        | Landing                               |
| 04 (4)        |                                       |
| 06 (6)        | Wind bullet                           |
| 07 (7)        | Wind bullet in air                    |
| 08 (8)        | Throwing Moo                          |
| 09 (9)        |                                       |
| 0A (10)       | Hurt                                  |
| 0B (11)       | Idle                                  |
| 0C (12)       |                                       |
| 0D (13)       | Idle w/ Moo                           |
| 0E (14)       | Helicopter Moo                        |
| 0F (15)       | Jumping w/ Moo                        |
| 10 (16)       | Walking w/ Moo                        |
| 11 (17)       |                                       |
| 12 (18)       |                                       |
| 13 (19)       |                                       |
| 14 (20)       | Fluttering                            |
| 15 (21)       |                                       |
| 16 (22)       |                                       |
| 17 (23)       |                                       |
| 18 (24)       |                                       |
| 19 (25)       |                                       |
| 1A (26)       |                                       |
| 1B (27)       | Double Jumping                        |
| 1C (28)       |                                       |
| 1D (29)       |                                       |
| 1E (30)       |                                       |
| 1F (31)       |                                       |
| 20 (32)       |                                       |
| 21 (33)       |                                       |
| 22 (34)       | Dead                                  |
| 23 (35)       |                                       |
| 24 (36)       |                                       |
| 25 (37)       |                                       |
| 26 (38)       |                                       |
| 27 (39)       |                                       |
| 28 (40)       | Grab green ball thing                 |
| 29 (41)       | Whirlpool (idk what it's called) jump |
