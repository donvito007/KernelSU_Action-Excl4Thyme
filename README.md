**中文** | [English](README_EN.md)

# KernelSU Action

用於 Non-GKI Kernel 的 Action，具有一定的普遍性，需要了解內核及 Android 的相關知識得以運用。

## 警告:warning: :warning: :warning:

如果你不是內核作者，使用他人的勞動成果構建 KernelSU，請僅供自己使用，不要分享給別人，這是對原作者的勞動成果的尊重。

## 支持內核

- `5.4`
- `4.19`
- `4.14`
- `4.9`

## 使用

> 所有 config.env 內的變數均只判斷`true`

> 編譯成功後，會在`Action`上傳 AnyKernel3，已經關閉設備檢查，請在 Twrp 刷入。

Fork 本倉庫到你的儲存庫然後按照以下內容編輯 config.env，之後點擊`Star`或`Action`，在左側可看見`Build Kernel`選項，點擊選項會看見右邊的大對話框的上面會有`Run workflows`點擊它會啟動構建。

### Kernel Source

修改為你的內核倉庫地址

例如: https://github.com/Diva-Room/Miku_kernel_xiaomi_wayne

### Kernel Source Branch

修改為你的內核分支

例如: TDA

### Kernel Config

修改為你的內核配置檔案名

例如: vendor/wayne_defconfig

### Arch

例如: arm64

### Kernel Image Name

修改為需要刷寫的 kernel binary，一般與你的 aosp-device tree 裡的 BOARD_KERNEL_IMAGE_NAME 是一致的

例如: Image.gz-dtb

常見還有 Image、Image.gz

### Clang

#### Use custom clang

可以使用除 google 官方的 clang，如[proton-clang](https://github.com/kdrag0n/proton-clang)

#### Custom Clang Source

> 如果是 git 倉庫，請填寫包含`.git`的連結

支持 git 倉庫或者 zip 壓縮包的直鏈

#### Custom cmds

都用自訂 clang 了，自己改改這些配置應該都會吧 :)

#### Clang Branch

由於 [#23](https://github.com/xiaoleGun/KernelSU_Action/issues/23) 的需要，我們提供可自訂 Google 上游分支的選項，主要的有分支有
| Clang 分支 |
| ---------- |
| master |
| master-kernel-build-2021 |
| master-kernel-build-2022 |

或者其它分支，請根據自己的需求在 https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86 中尋找

#### Clang version

填寫需要使用的 Clang 版本
| Clang 版本 | 對應 Android 版本 | AOSP-Clang 版本 |
| ---------- | ----------------- | --------------- |
| 12.0.5 | Android S | r416183b |
| 14.0.6 | Android T | r450784d |
| 14.0.7 | | r450784e |
| 15.0.1 | | r458507 |

一般 Clang12 就能通過大部分 4.14 及以上的內核的編譯
我自己的 MI 6X 4.19 使用的是 r450784d

### GCC

#### Enable GCC 64

啟用 GCC 64 交叉編譯

#### Enable GCC 32

啟用 GCC 32 交叉編譯

### Extra cmds

有的內核需要加入一些其它編譯命令，才能正常編譯，一般不需要其它的命令，請自行搜索自己內核的資料
請在命令與命令之間用空格隔開

例如: LLVM=1 LLVM_IAS=1

### Enable KernelSU

啟用 KernelSU，用於排查內核故障或單獨編譯內核

#### KernelSU Branch or Tag

選擇 KernelSU 的分支或 tag:

- main 分支(開發版): `KERNELSU_TAG=main`
- 最新 TAG(穩定版): `KERNELSU_TAG=`
- 指定 TAG(如`v0.5.2`): `KERNELSU_TAG=v0.5.2`

### Disable LTO

LTO 用於最佳化內核，但有些時候會導致錯誤

### Disable CC_WERROR

用於修復某些不支持或關閉了Kprobes的內核，修復KernelSU未檢測到開啟Kprobes的變數拋出警告導致錯誤

### Add Kprobes Config

自動在 defconfig 注入參數

### Add overlayfs Config

此參數為 KernelSU 模組和 system 分區讀寫提供支持
自動在 defconfig 注入參數

### Enable ccache

啟用快取，讓第二次編譯內核更快，最少可以減少 2/5 的時間

### Need DTBO

上傳 DTBO
部分設備需要

### Build Boot IMG

> 從之前的 Workflows 合併進來的，可以查看歷史提交

編譯 boot.img，需要你提供`Source boot image`

### Source Boot Image

故名思義，提供一個源系統可以正常開機的 boot 鏡像，需要直鏈，最好是同一套內核原始碼以及與你當前系統同一套設備樹從 aosp 構建出來的。ramdisk 裡面包含分區表以及 init，沒有的話構建出來的鏡像會無法正常引導。

例如: https://raw.githubusercontent.com/xiaoleGun/KernelSU_action/main/boot/boot-wayne-from-Miku-UI-latest.img

## 感謝

- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [KernelSU](https://github.com/tiann/KernelSU)
- [xiaoxindada](https://github.com/xiaoxindada)
