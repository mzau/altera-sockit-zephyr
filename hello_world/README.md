# Build recipe to reproduce the problem #

## load environment ##
<pre>
source $HOME/github.com/zephyr/zephyr-env.sh
</pre>

## building and running ##
<pre>
mkdir build   # if not already there
cd build
cmake -GNinja -DBOARD=sockit ..
ninja
</pre>

## Output ##
<pre>
[4/87] Preparing syscall dependency handling

[82/87] Linking C executable zephyr/zephyr_prebuilt.elf
FAILED: : && ccache /home/za/zephyr-sdk/sysroots/x86_64-pokysdk-linux/usr/bin/nios2-zephyr-elf/nios2-zephyr-elf-:
Memory region         Used Size  Region Size  %age Used
           RESET:          0 GB         32 B      0.00%
            SRAM:  1073885580 B 18446744072640004064 B      0.00%
        IDT_LIST:          25 B         2 KB      1.22zephyr/libzephyr.a(exception.S.obj): In function `on_irq_s:
/home/za/github.com/zephyr/arch/nios2/core/exception.S:108:(.exception.entry._exception+0x7c): relocation trunca'
zephyr/libzephyr.a(exception.S.obj): In function `_exception_enter_fault':
/home/za/github.com/zephyr/arch/nios2/core/exception.S:179:(.exception.entry._exception+0xac): relocation trunca'
collect2: error: ld returned 1 exit status
%
ninja: build stopped: subcommand failed.
</pre>

*Besides the relocation problem the strange thing here is the giant region size for the SRAM.*

# Build recipe for altera MAX10 board #
<pre>
cd $ZEPHYR_BASE/samples/hello_world
mkdir build
cd build
cmake -GNinja -DBOARD=altera_max10
ninja
</pre>
## Output with altera MAX10 board ##

<pre>
[4/90] Preparing syscall dependency handling

[85/90] Linking C executable zephyr/zephyr_prebuilt.elf
Memory region         Used Size  Region Size  %age Used
           RESET:          28 B         32 B     87.50%
           FLASH:       10088 B     753632 B      1.34%
            SRAM:        4268 B     131040 B      3.26%
        IDT_LIST:          25 B         2 KB      1.22%
[90/90] Linking C executable zephyr/zephyr.elf
</pre>

