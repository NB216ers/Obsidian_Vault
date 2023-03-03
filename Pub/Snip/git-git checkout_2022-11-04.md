git-git checkout
date:2022-11-04 16:01

```md
放弃修改 如果不指定切换到哪个分支，那就是切换到当前分支，虽然HEAD的指向没有变化，但是后面的两个恢复过程依然会执行，于是就可以理解为放弃index和工作区的变动。但是出于安全考虑 git 会保持 index 的变动不被覆盖。

1、只放弃工作区的改动，index 保持不变，其实就是从当前 index 恢复 工作区：  
	放弃工作区中全部的修改 git checkout .  
	放弃工作区中某个文件的修改： git checkout -- filename  
	先使用 git status 列出文件，然后 git checkout -- app/Http/Controllers/Read/Read3Controller.php  

2、强制放弃 index 和 工作区 的改动：  git checkout -f  这是不可逆的操作，会直接覆盖，但是还是很有用的，有时候想放弃这些改动，使用svn的时候可以直接把文件删掉再update，但是使用git就不能这么操作，使用 git checkout 可以满足这一点。
```