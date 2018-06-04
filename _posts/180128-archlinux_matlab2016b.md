#archlinux matlab2016b
January 28, 2018 6:38 PM
参考[《Ubuntu 16.04 LTS下安装MATLAB R2016b》](http://blog.csdn.net/dr_destiny/article/details/53336324)
1. 创建个临时目录`mkdir /home/qiangge/MATLABtmp`
2. 管理员权限挂载，否则无法加选项，`sudo mount -t auto -o loop /home/qiangge/soft/w@MMaR16b_Lin64/R2016b_glnxa64_dvd1.iso /home/qiangge/MATLABtmp`
3. 要在本机操作，而不是ssh或者远程桌面。在home目录运行install文件，在光盘运行是不允许的。远程桌面也是不可以的。
4. 果然是正好在80%的时候要求插入第二张光盘`sudo mount -t auto -o loop /home/qiangge/soft/w@MMaR16b_Lin64/R2016b_glnxa64_dvd2.iso /home/qiangge/MATLABtmp`，但是安装到90%的时候失败。
5. 按照自带的安装指导输入如下命令依然失败，`sudo /home/qiangge/MATLABtmp/install -inputFile installer_input_qiangge.txt`
6. 继续[参考资料](https://zhuanlan.zhihu.com/p/23633624)改到如下命令看起来不错`sudo /home/qiangge/MATLABtmp/install -destinationFolder /usr/local/Matlab2016b/ -fileInstallationKey 09806-07443-53955-64350-21751-41297 -agreeToLicense yes -outputFile /tpm/mathworks_qiangge02.log -mode silent -activationPropertiesFile /home/qiangge/soft/w@MMaR16b_Lin64/crack/license_standalone.lic`

sudo umount –l /home/qiangge/MATLABtmp
sudo mount –o loop R2016b_glnxa64_dvd2.iso /home/qiangge/MATLABtmp

后来安装了多次，老是失败，无论是图形界面还是命令行，最后估计是安装包中某个产品出现了问题。最后是有选择的安装的，这样就OK了。安装的结果为只是安装了自己需要的部分，完成后，首先启动一次matlab看看，果然要激活，几遍手动制定了激活文件也没用，估计要管理员权限，额米有测试，后来按照破解思路，就是讲破解文件的四个库文件拷贝覆盖，然后新建个目录放进去lic文件即可。

参考资源很重要。。。
