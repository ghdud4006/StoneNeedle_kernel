# StoneNeedle_kernel
base: linux 3.13 kernel (https://mirrors.edge.kernel.org/pub/linux/kernel/v3.x/)



Adding Ctags & Cscope
>make ctags  
>find "$PWD" -name "\*.c" -o -name "\*.h" | cscope -q -R -b




## 일단 int 형으로 buffer_head 랑 bio 에 fs_component_type 라는 필드 파놓음 
0 : superblock 
1 : group descriptor
2 : block bitmap
3 : inode bitmap
4 : inode
5 : data block
6 : journal

