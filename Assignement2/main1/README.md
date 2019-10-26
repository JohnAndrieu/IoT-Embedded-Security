# Assignement 2
## Part 1 - Cross toolchains

## Part 2 - Reverse engineer raw binary blobs
### Arch 1 - ARM
The first architecture seems to be ARM. When diassembling the file A with big endian, we can find the substraction instruction with 0xface.

![ARM-big-disass](img/arch1fileA-arm-big.png)

We can see @0x1c and @0x20 the two SUB with 0xfa00 and 0xce. We can now disassemble the file B in little endian to find the same thing.

![ARM-little-disass](img/arch1fileB-arm-little.png)

### Arch 2 - MIPS
The second architecture looks like MIPS. We can disassemble the file C in little endian. the `li` instruction is the "Load imediate" instruction, used to load value in a register, here the `v0` register. Just after, @0x1c, this register is added with the register `v1`.

![MIPS-little-disass](img/arch2fileC-mips-little.png)

Now we can disassemble the file D in big endian.

![MIPS-big-disass](img/arch2fileD-mips-big.png)

### Arch 3 - PowerPC
Now we can try the last arch, PowerPC.

![POWERPC-big-disass](img/arch3fileE-powerpc-big.png)

@0x10, we see a 0 being loaded in the register r0. After this, we can see the `ori` instruction, that will apply a `or` between 0xcafe (0d51966) and r0, which is currently 0. So basically, 0xcafe is being loaded in r0 register. Right after, the `mr` instruction is used to move the content of r0 into r3 register, which is the [return register](https://www.ibm.com/support/knowledgecenter/en/ssw_aix_72/assembler/idalangref_reg_use_conv.html).

## Part 3 - Cross-compile simple program
### ARM

For the ARM architecutre, simply run in the bin folder
```bash
./arm-unknown-linux-gnueabi-gcc ../../../../exercise2/exercise2_main/file.c -o arm_bigendian.o -c -mbig-endian
./arm-unknown-linux-gnueabi-gcc ../../../../exercise2/exercise2_main/file.c -o arm_littleendian.o -c -mlittle-endian
```
After this, we can check the file type like this

![littleendian](img/littleendian.png)

![bigendian](img/bigendian.png)

### s390x

For the x390x architecture, simply run this command in the bin folder

```bash
./s390x-linux-gcc ../../../../exercise2/exercise2_main/file.c -o s390x.o -c
```

We can check the result like this 

![s309x](img/s390x.png)