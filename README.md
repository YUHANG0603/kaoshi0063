#include <reg51.h>
sbit wela_left = P2^0;  
sbit wela_right = P2^1; 
unsigned char code seg_table[] = {0xC0, 0xF9, 0xA4, 0xB0, 0x99, 0x92, 0x82, 0xF8, 0x80, 0x90};
unsigned int count = 0; 
unsigned char sec = 60;  

void timer0_init() {
    TMOD = 0x01;        
    TH0 = 0xFC;        
    TL0 = 0x66;
    ET0 = 1;            
    EA = 1;             
    TR0 = 1;            
}
void display() {
    unsigned char shi = sec / 10; 
    unsigned char ge = sec % 10; 
    unsigned int i;
    wela_right = 0;       
    P0 = seg_table[shi]; 
    wela_left = 1;       
    for(i=50; i>0; i--); 
    wela_left = 0;
    wela_left = 0;        
    P0 = seg_table[ge]; 
    wela_right = 1;
    for(i=50; i>0; i--);
    wela_right = 0;
}
void timer0_isr() interrupt 1 {
    TH0 = 0xFC;          
    TL0 = 0x66;
    count++;
if(count >= 1000) {  
        count = 0;
        sec = (sec > 0) ? (sec - 1) : 0;
        if(sec == 0) TR0 = 0; 
    }
}
void main() {
    timer0_init();       
    while(1) {
        display();        
    }
}
