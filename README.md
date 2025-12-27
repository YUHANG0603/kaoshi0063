#include <reg51.h>
#define jzkey P1
sbit weixuan = P3^0;
unsigned char xianshi = 0;
void delay(unsigned int t)
{
    unsigned int i, j;
    for(i=0; i<t; i++)
        for(j=0; j<127; j++);
}
void anjian()
{
    unsigned char a = 0;
    jzkey = 0x0f;
    if(jzkey != 0x0f)
    {
        delay(10);
        if(jzkey != 0x0f)
        {
            switch(jzkey)
            {
                case 0x07: xianshi = 0; break;
                case 0x0b: xianshi = 1; break;
                case 0x0d: xianshi = 2; break;
                case 0x0e: xianshi = 3; break;
            }
            jzkey = 0xf0;
            switch(jzkey)
            {
                case 0x70: xianshi += 0; break;
                case 0xb0: xianshi += 4; break;
                case 0xd0: xianshi += 8; break;
                case 0xe0: xianshi += 12; break;
            }
            while((a<50) && (jzkey!=0xf0))
            {
                delay(10);
                a++;
            }
        }
    }
}
void main()
{
    weixuan = 0;
    while(1)
    {
        anjian();
        switch(xianshi)
        {
            case 0: P2 = 0x3f; break; // 0
            case 1: P2 = 0x06; break; // 1
            case 2: P2 = 0x5b; break; // 2
            case 3: P2 = 0x4f; break; // 3
            case 4: P2 = 0x66; break; // 4
            case 5: P2 = 0x6d; break; // 5
            case 6: P2 = 0x7d; break; // 6
            case 7: P2 = 0x07; break; // 7
            case 8: P2 = 0x7f; break; // 8
            case 9: P2 = 0x6f; break; // 9
            case 10: P2 = 0x77; break; // A
            case 11: P2 = 0x7c; break; // b
            case 12: P2 = 0x39; break; // C
            case 13: P2 = 0x5e; break; // d
            case 14: P2 = 0x79; break; // E
            case 15: P2 = 0x71; break; // F
            default: P2 = 0x00; break;
        }
    }
}
