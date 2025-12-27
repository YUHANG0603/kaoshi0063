#include <reg51.h>
#define LCD_DATA_PORT P2
sbit RS = P3^0;  // 寄存器选择信号
sbit RW = P3^1;  // 读写控制信号
sbit EN = P3^2;  // 使能控制信号
void delay_ms(unsigned int ms) {
    unsigned int i, j;
    for(i = 0; i < ms; i++)
        for(j = 0; j < 1275; j++);
}
// 向LCD发送命令
void lcd_write_command(unsigned char cmd) {
    RS = 0;     // 命令模式
    RW = 0;     // 写操作
    LCD_DATA_PORT = cmd; // 发送命令
    EN = 1;     // 使能
    delay_ms(1);
    EN = 0;     // 存锁命令
    delay_ms(2);
}
// LCD发送数据
void lcd_write_data(unsigned char dat) {
    RS = 1;     // 数据模式
    RW = 0;     // 写操作
    LCD_DATA_PORT = dat; // 发送数据
    EN = 1;     // 使能
    delay_ms(1);
    EN = 0;     // 存锁数据
    delay_ms(2);
}
// LCD初始化函数
void lcd_init() {
    delay_ms(20); // 上电延时
    lcd_write_command(0x38); // 8位数据口，2行显示，5*8点阵
    lcd_write_command(0x0c); // 显示开，光标关
    lcd_write_command(0x06); // 文字不动地址+1
    lcd_write_command(0x01); // 清屏
    delay_ms(2);
}
// 字符显示函数
void lcd_show_string(unsigned char x, unsigned char y, unsigned char *str) {
    // 设置显示位
    if(y == 0)
        lcd_write_command(0x80 + x);
    else
        lcd_write_command(0xc0 + x);
// 发送字符
    while(*str != '\0') {
        lcd_write_data(*str);
        str++;
    }
}
void main() {
    unsigned char english_str[] = "123";
    lcd_init();
    lcd_show_string(0, 0, english_str);
    while(1);
}
