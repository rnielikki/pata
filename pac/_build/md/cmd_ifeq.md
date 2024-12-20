# cmd_ifEQ

Compares two values and jumps to a specific instruction (without executing next) if the value is equal to the other one.

## Code Information

- **Name**: `cmd_ifEQ`
- **Scope**: Global
- **PAC Instruction (Binary)**: `25 00 17 00`
- **Assembly Address in Memory** : `0x88388ac`

## Parameters

`cmd_ifEQ((int/float)value1, (int/float)value2, (Address)address)`

- `(Int/Float)value1` *(8 bytes)* : A value to compare. Can be variable or immediate. Read-only.
- `(Int/Float)value2` *(8 bytes)* : The another value to compare. Can be variable or immediate. Read-only.
- `(Address)address` *(4 bytes)* : Address to jump, the address is hex instruction offset from the PAC file.

This performs `if(value1 == value2) goto address;`

## Remarks

For int/float, the function converts the type automatically.

## Example

Here is one example in hex:

```25 00 17 00 / 04 00 00 00 / 00 00 00 00 / 10 00 00 00 / 00 00 00 40 / 58 03 00 00```

Which is interpreted as:

```c
cmd_ifEQ((int *)iVar0, (float)2, 0x358)
```

## Code

Ths PAC instruction calls this function (Decompiled by Ghidra):

```c
void FUN_088388ac(undefined4 param_1,undefined4 param_2)

{
  float *pfVar1;
  float *pfVar2;
  undefined4 *puVar3;
  uint uVar4;
  uint uVar5;
  float fVar6;
  
  pfVar1 = (float *)Pac_Get_Param(param_2,0,1,4);
  pfVar2 = (float *)Pac_Get_Param(param_2,1,1,4);
  puVar3 = (undefined4 *)Pac_Get_Param(param_2,2,0,4);
  uVar4 = Pac_Get_ParamType(param_2,0);
  uVar5 = Pac_Get_ParamType(param_2,1);
  if ((uVar4 & 0x70) == 0) {
    if ((uVar5 & 0x70) == 0) {
      fVar6 = *pfVar2;
    }
    else {
      fVar6 = (float)(int)*pfVar2;
    }
    if (*pfVar1 == fVar6) {
      PAC::Cmd_Jump_Or_Call(param_2,*puVar3,0);
    }
  }
  else {
    if ((uVar5 & 0x70) == 0) {
      fVar6 = (float)(int)*pfVar2;
    }
    else {
      fVar6 = *pfVar2;
    }
    if (*pfVar1 == fVar6) {
      PAC::Cmd_Jump_Or_Call(param_2,*puVar3,0);
    }
  }
  PAC::PAC_setCmdId(param_2,0);
  return;
}
```

