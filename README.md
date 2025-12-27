#include <reg51.h>
#define uint unsigned int
#define uchar unsigned char
sbit WLE=P2^6;
sbit DLE=P2^7;
uchar code table[]={0x3f,0x06,0x5b,0x4f,0x66,0x6d,0x7d,0x07,0x7f,0x6f,0x77,0x7c,0x39,0x5e,0x79,0x71};
uchar code pos[]={0xf0,0xfe,0xfe,0xfd,0xfb,0xf7,0xef,0xdf,0xbf,0x7f};
uchar n;
void delay(uint z)
{
    uint x,y;
    for(x=z;x>0;x--)
        for(y=12;y>0;y--);
}
void main()
{
    while(1)
    {
        for(n=1;n<=8;n++)
        {
            if(n==1)
            {
                WLE=1;
                P0=pos[n];
                WLE=0;
                DLE=1;
                P0=table[n];
                DLE=0;
                delay(1000);
            }
            else if(n==2)
            {
                WLE=1;
                P0=pos[n];
                WLE=0;
                DLE=1;
                P0=table[n];
                DLE=0;
                delay(1000);
            }
            else if(n==3)
            {
                WLE=1;
                P0=pos[n];
                WLE=0;
                DLE=1;
                P0=table[n];
                DLE=0;
                delay(1000);
            }
            else if(n==4)
            {
                WLE=1;
                P0=pos[n];
                WLE=0;
                DLE=1;
                P0=table[n];
                DLE=0;
                delay(1000);
            }
            else if(n==5)
            {
                WLE=1;
                P0=pos[n];
                WLE=0;
                DLE=1;
                P0=table[n];
                DLE=0;
                delay(1000);
            }
            else if(n==6)
            {
                WLE=1;
                P0=pos[n];
                WLE=0;
                DLE=1;
                P0=table[n];
                DLE=0;
                delay(1000);
            }
            else if(n==7)
            {
                WLE=1;
                P0=pos[n];
                WLE=0;
                DLE=1;
                P0=table[n];
                DLE=0;
                delay(1000);
            }
            else if(n==8)
            {
                WLE=1;
                P0=pos[n];
                WLE=0;
                DLE=1;
                P0=table[n];
                DLE=0;
                delay(1000);
            }
        }
    }
}
