
# 什么是 umask?

当我们登录系统之后创建一个文件总是有一个默认权限的，那么这个权限是怎么来的呢？这就是umask干的事情。umask设置了用户创建文件的默认 权限，它与chmod的效果刚好相反，umask设置的是权限“补码”，而chmod设置的是文件权限码。一般在/etc/profile、$ [HOME]/.bash_profile或$[HOME]/.profile中设置umask值。

你的系统管理员必须要为你设置一个合理的 umask值，以确保你创建的文件具有所希望的缺省权限，防止其他非同组用户对你的文件具有写权限。在已经登录之后，可以按照个人的偏好使用umask命 令来改变文件创建的缺省权限。相应的改变直到退出该shell或使用另外的umask命令之前一直有效。一般来说，umask命令是在/etc /profile文件中设置的，每个用户在登录时都会引用这个文件，所以如果希望改变所有用户的umask，可以在该文件中加入相应的条目。如果希望永久 性地设置自己的umask值，那么就把它放在自己$HOME目录下的.profile或.bash_profile文件中。

[参考]([umask命令详解 - 马昌伟 - 博客园 (cnblogs.com)](https://www.cnblogs.com/machangwei-8/p/10354563.html))