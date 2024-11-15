# getClassType

Gets handle type of the given handle.

This is **not** for obtaining unit class.

## Code Information

- **Name**: `getClassType`
- **Scope**: Global
- **PAC Instruction (Binary)**: `25 17 53 00`
- **Assembly Address in Memory** : `0x89170b4`

## Parameters

- `(int *)handle` *(8 bytes)* : Handle from various places.
- `(int *)handle_type` *(8 bytes)* : Variable to *store* the handle. If it is invalid unit, the value is -1.

|`handle_type`|handle|
|---|---|
|`0x2`|Troop|
|`0x3`|Squad|
|`0x9`|Unit/Character (or bubble speech handle is also 0x9, just why)|
|`0xA`|Gimmick|
|`0xB`|Effect|

## Example

Here is one example in hex:

```25 17 53 00 / 04 00 00 00 / 41 00 00 00 / 04 00 00 00 / 00 00 00 00```

Which is interpreted as:

```c
getClassType((int *)iVar65, (int *)iVar0)
```

## Code

Ths PAC instruction calls this function (Decompiled by Ghidra):

```c
void FUN_089170b4(int param_1,undefined4 param_2)

{
  int *piVar1;
  undefined4 *puVar2;
  int iVar3;
  undefined4 uVar4;
  
  piVar1 = (int *)Pac_Get_Param(param_2,0,1,4);
  puVar2 = (undefined4 *)Pac_Get_Param(param_2,1,1,4);
  *puVar2 = 0xffffffff;
  if (*piVar1 != -1) {
    iVar3 = Find_Target_By_HandleID(*(undefined4 *)(param_1 + 0x14),*piVar1,1);
    if (iVar3 == 0) {
      iVar3 = 0;
    }
    if (iVar3 != 0) {
      uVar4 = (**(code **)(*(int *)(iVar3 + 4) + 0x34))(iVar3);
      *puVar2 = uVar4;
    }
  }
  PAC::PAC_setCmdId(param_2,0);
  return;
}
```

