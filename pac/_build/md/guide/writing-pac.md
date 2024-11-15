# How to (over)write a PAC instruction

As I said "I am assuming you are asking about modifying. Writing from the bottom is terrifying."<br>
This is about modifying existing PAC instruction.

Since there are bunch of common condition checking and resource/effect loading, writing from bottom is very very discouraged and you couldn't do it anyway.

Also, always **check context of the parameter** before assigning any parameter. Otherwise it might cause potential disaster.

small local parameter indexes like 0, 1, 2, 3 (e.g. `04 00 00 00 01 00 00 00`) are potentially temporary parameters that can be changed at any time.

## Case 1: Your code occupies less space

Easy, you can just fill `00` in empty spaces.

Just try to fill zero **just BEFORE `25 XX XX XX`**, which is next PAC instruction.

## Case 2: Your code occupies same space

Just overwrite them.

## Case 3: Your code occupies more space

**Do not insert from the middle**. Always **append** at the end of the file.

The edited PAC file size can be bigger than original, and there is no issue with the size.<br>
(Unless the file size is very big so doesn't fit to the memory, which is not ordinary)

Another approach is replacing unused part like debug mode code (be sure to make debug mode inaccessible in this case).

### 1. Using cmd_jmp

1. Pick the instruction *after* the position you want to insert. If the one instruction is only 4 bytes, pick two instructions.
2. Replace it to [cmd_jmp](../cmd_jmp.md) that goes to **end of the file**.
3. Insert your code **in end of the file**.
4. Put the *original instruction(s) from step 1* to the end of the file.
5. **Put the `cmd_jmp`** to the end of the file!

### 2. Using cmd_call (Recommended)

1. Pick the instruction *after* the position you want to insert. If the one instruction is only 4 bytes, pick two instructions.
2. Replace it to [cmd_call](../cmd_call.md) that goes to **end of the file**.
3. Insert your code **in end of the file**.
4. Put the *original instruction(s) from step 1* to the end of the file.
5. **Put `[cmd_end](../cmd_end.md)`** to the end of the file!


**DO NOT extend from the middle of the file**!<br>
It will mess up a lot of jump and call condition (reminder they use offset from PAC file).