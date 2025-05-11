# 关于这个仓库

本仓库是适用于小米 SM8250 系列机型的 4.19 内核，Fork 自[Strawing老哥的仓库](https://github.com/liyafe1997/kernel_xiaomi_sm8250_mod)

该内核主要基于[Lineage OS 22 xiaomi sm8250 kernel source](https://github.com/LineageOS/android_kernel_xiaomi_sm8250)，MIUI特性的代码以及部分的设备驱动抠自[UtsavBalar1231 老哥的仓库](https://github.com/UtsavBalar1231/kernel_xiaomi_sm8250)

感谢[yspbwx2010](https://github.com/yspbwx2010/kernel_xiaomi_sm8250_mod)老哥维护的分支，修复了[电量卡在1%的问题](https://github.com/liyafe1997/Xiaomi-fix-battery-one-percent)，并提供了带KernelSU的预编译好的内核，添加更多功能并优化性能与功耗，以及一个更直观和易用的编译脚本和README，方便大家自己折腾和修改，编译自己的内核！
(其中受“1%电量bug”影响的设备有：alioth, apollo, lmi, thyme, umi, pipa，因为它们都用了PM8150即高通的GEN4电量计。其它不受此bug影响的设备大可把这个内核当成个带KernelSU的官核平替，如果你想找一个带KernelSU的内核的话。并且据大家测试，该内核不带KernelSU版本可以应用[APatch](https://github.com/bmax121/APatch))

Release里的编译好的内核成品由`android14-lineage22-mod`分支编译，应当能在原版MIUI和第三方的基于AOSP的各种Android11-14的ROM上使用，部分设备在Android15上会有非常严重的问题。欢迎大家尝试并反馈(提交 Issue 或 Pull Requests)！酷友们到[酷安的这个帖子](https://www.coolapk.com/feed/56813047)讨论或反馈，也可以给 Strawing 老哥或我私信反馈！

支持的设备:
| 设备代号  | 设备名称                           |
|-----------|----------------------------------|
| psyche    | 小米12X                           |
| thyme     | 小米10S                           |
| umi       | 小米10                            |
| munch     | 红米K40S                          |
| lmi       | 红米K30 Pro                       |
| cmi       | 小米10 Pro                        |
| cas       | 小米10 Ultra                      |
| apollo    | 小米10T / 红米K30S Ultra          |
| alioth    | 小米11X / POCO F3 / 红米K40       |
| elish     | 小米平板5 Pro                     |
| enuma     | 小米平板5 Pro 5G                  |
| dagu      | 小米平板5 Pro 12.4                |
| pipa      | 小米平板6                         |

该内核的其他特性/改进:
1. 支持USB串口驱动（CH340/FTDI/PL2303/OTI6858/TI/SPCP8X5/QT2/UPD78F0730/CP210X）
2. 支持EROFS
3. 更新了官方最新的触摸屏固件
4. F2FS开启了Realtime Discard以更好的TRIM闪存，还有 ATGC 和 GC_MERGE
5. 支持 CANBus 和 USB CAN （如 CANable）适配器（一些折腾嵌入式的可能会喜欢这个）
6. 更新的 ZSTD 和 LZ4
7. ZSTD 支持在用户空间调整压缩等级
8. ZRAM 支持 LZO,LZO-RLE,LZ4,LZ4HC,LZ4K,LZ4KD,842.DEFLATE,ZSTD 压缩算法
9. 引入 Sultan 的 [Simple_LMK](https://github.com/kerneltoast/simple_lmk)
10. PELT 半衰期锁定为 16ms 以降低功耗
11. 开启 UFS 读写增强器，优化读写速度
12. 添加了 LXC/Docker 补丁，支持容器运行
13. 集成了 NTFS, EXFAT, EROFS, SQUASHFS, NFS, SMB(CIFS), CD/DVD 等多种文件系统支持，可根据需要开启（部分文件系统支持存在问题，未验证/待修复）
14. 为 SukiSU 添加了 VFS钩子/附加环境补丁
15. 其他各种各样的优化......

注意：该内核的zip包不包含`dtbo.img`，并且不会刷你的dtbo分区。推荐使用原厂的`dtbo`，或者来自第三方系统包自带的dtbo（如果原作者确认好用的话）。因为该源码build出来的`dtbo.img`有些小问题，比如在锁屏界面上尝试熄屏时，屏幕会突然闪一下到最高亮度。如果你刷过其它第三方内核，或者遇到一些奇怪的问题，建议检查一下你的`dtbo`是否被替换过。

欢迎加入内测QQ群: 459094061

本仓库支持使用 Github Action 快速便捷地构建内核，步骤如下
1. Fork 本仓库
2. 点击上方 Action，并在左侧找到 Build Kernel 工作流
3. 点击右侧 Run workflow，配置你的机型和系统等选项
4. 点击下方绿色的 Run workflow 按钮，耐心等待一段时间
5. 最后就可以在 Release 里看到你的内核 AK3 卡刷包啦！
