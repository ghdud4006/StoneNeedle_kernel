# StoneNeedle_kernel
base: linux 3.13 kernel (https://mirrors.edge.kernel.org/pub/linux/kernel/v3.x/)



Adding Ctags & Cscope
>make ctags  
>find "$PWD" -name "\*.c" -o -name "\*.h" | cscope -q -R -b




## 일단 int 형으로 buffer_head->fs_component_type, bio->fs_component_type 라는 필드 파놓음 

0 : superblock  
1 : group descriptor - ext4_fill_super(), [Link](https://github.com/ghdud4006/StoneNeedle_kernel/commit/63201855d557eeeeb517d77cb8af3356cc2a74e1)

2 : block bitmap  
3 : inode bitmap  
4 : regular file inode  
5 : directory inode  
6 : regular file data block  
7 : directory data block  
8 : journal data  

아래 코드로 StoneNeedle 모듈이 bio 로부터 type 받으니 참고  

```c
  /* superblock */
  	if (bio->fs_component_type == 0)
		calc_bucket_account(io_data->write_ext4_sb_per_chunk, bio,
			    io_data->bucket_size);
	/* group descriptor */
	else if (bio->fs_component_type == 1) 
		calc_bucket_account(io_data->write_ext4_grdesc_per_chunk, bio,
			    io_data->bucket_size);	
	/* block bitmap */
	else if (bio->fs_component_type == 2) 
		calc_bucket_account(io_data->write_ext4_bbmap_per_chunk, bio,
			    io_data->bucket_size);
	/* inode bitmap */
	else if (bio->fs_component_type == 3) 
		calc_bucket_account(io_data->write_ext4_ibmap_per_chunk, bio,
			    io_data->bucket_size);
	/* regular file inode */
	else if (bio->fs_component_type == 4) 
		calc_bucket_account(io_data->write_ext4_rinode_per_chunk, bio,
			    io_data->bucket_size);
	/* directory inode */
	else if (bio->fs_component_type == 5) 
		calc_bucket_account(io_data->write_ext4_dinode_per_chunk, bio,
			    io_data->bucket_size);
	/* regular file data block */
	else if (bio->fs_component_type == 6) 
		calc_bucket_account(io_data->write_ext4_rblock_per_chunk, bio,
			    io_data->bucket_size);
	/* directory data block */
	else if (bio->fs_component_type == 7) 
		calc_bucket_account(io_data->write_ext4_dblock_per_chunk, bio,
			    io_data->bucket_size);
	/* journal data */
	else if (bio->fs_component_type == 8) 
		calc_bucket_account(io_data->write_ext4_journal_per_chunk, bio,
			    io_data->bucket_size);
	/* undefined */
	else  
		return 0;
```
