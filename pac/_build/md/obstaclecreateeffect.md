# obstacleCreateEffect

**Description** goes here.

This page is automatically generated and not reviewed yet.<br>Remove this text if this page is fully reviewed.

## Code Information

- **Name**: `obstacleCreateEffect`
- **Scope**: Global
- **PAC Instruction (Binary)**: `25 21 35 00`
- **Assembly Address in Memory** : `0x89b42e0`

## Parameters

- `(undefined4)Var0` *(8 bytes)*

## Example

Here is one example in hex:

```25 21 35 00 / 04 00 00 00 / 14 00 00 00```

Which is interpreted as:

```c
obstacleCreateEffect((int *)iVar20)
```

## Code

Ths PAC instruction calls this function (Decompiled by Ghidra):

```c
void FUN_089b42e0(undefined4 param_1,undefined4 param_2)

{
  undefined4 *puVar1;
  int iVar2;
  
  puVar1 = (undefined4 *)Pac_Get_Param(param_2,0,1,4);
  iVar2 = Is_Valid_SquadHandle(param_1,*puVar1);
  if (iVar2 != 0) {
    (**(code **)(*(int *)(iVar2 + 0xc) + 0x120))(iVar2);
  }
  PAC::PAC_setCmdId(param_2,0);
  return;
}
```

