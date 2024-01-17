#pragma mark - 内联汇编退出程序函数 （直接调用即可）
void interrupt() {
#ifdef __arm64__
    asm(
        "mov x0, #0\n"  // 将 x0 寄存器设置为 0，通常用作函数参数
        "mov x16, #1\n" // 将 x16 寄存器设置为 1，代表 Sys_exit，即退出系统调用
        "svc #0x80\n"   // 调用软中断，触发系统调用
    );
#endif

#ifdef __arm__
    asm(
        "mov r0, #0\n"  // 将 r0 寄存器设置为 0，通常用作函数参数
        "mov r16, #1\n" // 将 r16 寄存器设置为 1，代表 Sys_exit，即退出系统调用
        "svc #80\n"     // 调用软中断，触发系统调用
    );
#endif
}
