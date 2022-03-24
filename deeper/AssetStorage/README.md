## File : `AssetStorage.txt`

This file holds assets directory. Example file:

```
~4182764457
@FgoDataVersion0066,20160420_1,20191217_11:54
1,DATA0,381064,1737938264,Audio/Servants_100300.cpk.bytes
1,SYSTEM,112832,89377592,CharaGraph/100000
```

1. First line
```
~4182764457
```
- `4182764457`: CRC32 in decimal of the rest of the file

2. Second line
```
@FgoDataVersion0066,20160420_1,20191217_11:54
```
- `FgoDataVersion0066`: MasterDataCacheVer
- `20160420_1`: dataVersion
- `20191217_11:54`: dateVersion

3. Asset data line
```
1,DATA0,15520,2437962836,NoblePhantasm/Sequence/401500
```
- `1`:
- `DATA0` or `SYSTEM`:
  - `SYSTEM`: required download before playing the game
  - `DATA0`: optional download
- `15520`: Encrypted asset size in bytes
- `2437962836`: CRC32 in decimal of the encrypted asset
- `NoblePhantasm/Sequence/401500`: Unencrypted name of the asset