# StoneNeedle_kernel
base: linux 3.13 kernel (https://mirrors.edge.kernel.org/pub/linux/kernel/v3.x/)



Adding Ctags & Cscope
>make ctags
>find "$PWD" -name "*.c" -o -name "*.h" | cscope -q -R -b
