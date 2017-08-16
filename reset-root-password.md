# 恢复 root 密码

在 Red Hat Enterprise Linux 7 / CentOS 7 系统，可以通过进入 **initramfs** 重新设置丢失的 root 密码：
1. 重启系统；
2. 按任意键中止 GRUB 的自动引导；
3. 将光标移动到引导项，通常是第一项；
4. 按 **"e"** 键编辑引导项；
5. 移动到以 **linux16** 开头的那一行；
6. 按 **ENTER** 键去到行尾，空格之后添加 **rd.break**
7. 最后按 **Ctrl-x** 引导系统

当进入系统之后，通过以下步骤重新设置 **root** 密码：
1. 读写方式重新挂载 **/sysroot**
    ```bash
    mount -oremount,rw /sysroot
    ```
2. 切换文件系统到 **/sysroot**
    ```bash
    chroot /sysroot
    ```
3. 设置新密码
    ```bash
    passwd
    ```
4. 为所有未标记的文件重新打标记
    ```bash
    touch /.autorelabel
    ```
5. 按两次 **Ctrl-D** 重启系统让密码生效。
