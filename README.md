#include <reg51.h>
#define LCD_DATA_PORT P2
sbit RS = P3^0;  
sbit RW = P3^1;  
sbit EN = P3^2;  
void delay_ms(unsigned int ms) {
    unsigned int i, j;
    for(i = 0; i < ms; i++)
        for(j = 0; j < 1275; j++);
}

void lcd_write_command(unsigned char cmd) {
    RS = 0;   
    RW = 0;    
    LCD_DATA_PORT = cmd; 
    EN = 1;   
    delay_ms(1);
    EN = 0;   
    delay_ms(2);
}
void lcd_write_data(unsigned char dat) {
    RS = 1;     
    RW = 0;    
    LCD_DATA_PORT = dat; 
    EN = 1;    
    delay_ms(1);
    EN = 0;    
    delay_ms(2);
}
void lcd_init() {
    delay_ms(20);
    lcd_write_command(0x38);
    lcd_write_command(0x0c); 
    lcd_write_command(0x06);
    lcd_write_command(0x01); 
    delay_ms(2);
}

void lcd_show_string(unsigned char x, unsigned char y, unsigned char *str) {

    if(y == 0)
        lcd_write_command(0x80 + x);
    else
        lcd_write_command(0xc0 + x);

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
