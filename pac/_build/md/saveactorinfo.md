# saveActorInfo

**Description** goes here.

This page is automatically generated and not reviewed yet.<br>Remove this text if this page is fully reviewed.

## Code Information

- **Name**: `saveActorInfo`
- **Scope**: Azito
- **PAC Instruction (Binary)**: `25 1c 1f 00`
- **Assembly Address in Memory** : `0x8b4f8a8`

## Parameters

- `(int)Var0` *(8 bytes)*
- `(undefined4)Var1` *(8 bytes)*

## Example

Usage not found for this function.

## Code

Ths PAC instruction calls this function (Decompiled by Ghidra):

```c
void FUN_Azito__08b4f8a8(int param_1,undefined4 param_2)

{
  int *piVar1;
  undefined4 *puVar2;
  int iVar3;
  int iVar4;
  undefined4 uVar5;
  int iVar6;
  
  piVar1 = (int *)Pac_Get_Param(param_2,0,1,4);
  iVar6 = *piVar1;
  puVar2 = (undefined4 *)Pac_Get_Param(param_2,1,1,4);
  uVar5 = *puVar2;
  iVar3 = Save::Get_Save_BaseAddr(1);
  iVar3 = iVar6 * 0x18 + *(int *)(iVar3 + 0x50) + 0x297e0;
  if ((iVar3 != 0) &&
     (iVar4 = Find_Target_By_HandleID(*(undefined4 *)(*(int *)(*(int *)(param_1 + 0x10) + 0x174) + 0xe8),uVar5,
                           1), iVar4 != 0)) {
    FUN_Azito__08b4cdf0(iVar3,iVar6,iVar4);
  }
  PAC::PAC_setCmdId(param_2,0);
  return;
}
```

