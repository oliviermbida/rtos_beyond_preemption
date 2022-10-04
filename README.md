# rtos_beyond_preemption
-------------------------

RTOS beyond the preemptive scheduling algorithms.

Lets start by looking at how these algorithms are implemented with an example taken from `PREEMPT_RT` patches.
These are code changes made to turn the linux kernel into `Real-Time Preemption`.
You can already configure the linux kernel for various preemptive scheduling or none.

- PREEMPT_NONE
- PREEMPT_VOLUNTARY
- PREEMPT

[Kconfig](https://kernel.ubuntu.com/git/ubuntu/ubuntu-focal.git/tree/kernel/Kconfig.preempt)

Since `PREEMPT_RT` is to get closer to `RTOS`, we will use the example from an embedded platform i.e Nvidia Jetson platform.

The required items are:
- [Bootloader](https://developer.nvidia.com/embedded/l4t/r35_release_v1.0/release/jetson_linux_r35.1.0_aarch64.tbz2)
- [Rootfs (Filesystem)](https://developer.nvidia.com/embedded/l4t/r35_release_v1.0/release/tegra_linux_sample-root-filesystem_r35.1.0_aarch64.tbz2)
- [Kernel](https://developer.nvidia.com/embedded/l4t/r35_release_v1.0/sources/public_sources.tbz2)
- [Toolchain (Cross compiler)](http://releases.linaro.org/components/toolchain/binaries/7.3-2018.05/aarch64-linux-gnu/gcc-linaro-7.3.1-2018.05-x86_64_aarch64-linux-gnu.tar.xz)

If you want to get fully into embedded software development then you will need the full Board Support Package (BSP) for Nvidia Jetson embedded platform.
But the main focus is on applying `PREEMPT_RT` patches after looking inside the codes changes to see which files they touch and what those changes actually do to the kernel.

Summary of the steps to build the kernel are:

- Environment variables

      export CROSS_COMPILE=$HOME/rootfs/l4t-gcc/gcc-linaro-7.3.1-2018.05-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu-
      export TEGRA_KERNEL_OUT=./jetson_linux
      export LOCALVERSION=-tegra
    
- Building

  * Configure
  
        make ARCH=arm64 O=$TEGRA_KERNEL_OUT tegra_defconfig
  
  * Build
  
        make ARCH=arm64 O=$TEGRA_KERNEL_OUT -j4
  
  * Output (Custom kernel) 
  
        TEGRA_KERNEL_OUT/arch/arm64/boot/Image
        
[Step-by-step guide](https://docs.nvidia.com/jetson/archives/l4t-archived/l4t-3231/index.html#page/Tegra%2520Linux%2520Driver%2520Package%2520Development%2520Guide%2Fkernel_custom.html%23) 




