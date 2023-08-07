# DAC-in-Embedded-C
SQUARE WAVE GENERATOR:
#include <LPC17xx.H>
57
#include "GLCD.H"
#define __FI 1 
void delay(void)
{
 unsigned char i;
 for(i=0;i<1000;i++);
}
main()
{ 
unsigned int i,j;
 LPC_SC->PCONP |= (1 << 15); 
LPC_GPIO0->FIODIR |= 0x007F8000; 
 LPC_GPIO1->FIODIR |= 0x07F80000;
#ifdef __USE_LCD
GLCD_Init(); 
GLCD_Clear(White); 
GLCD_SetBackColor(Blue);
GLCD_SetTextColor(White);
GLCD_DisplayString(0, 0, __FI, " ESA ");
GLCD_DisplayString(1, 0, __FI, " KRCE ");
GLCD_DisplayString(2, 0, __FI, " EMBEDDED LAB ");
GLCD_SetBackColor(White);
GLCD_SetTextColor(Blue);
GLCD_DisplayString(5, 0, __FI, " Dual DAC ");
GLCD_DisplayString(6, 0, __FI, " Square Wave ");
//#endif
while(1)
 {
for(i=0; i<0x0FF; i++)
 {
LPC_GPIO0->FIOPIN =(LPC_GPIO0->FIOPIN & 0xFF807FFF) | 0x007F8000; 
LPC_GPIO1->FIOPIN = (LPC_GPIO1->FIOPIN & 0xF807FFFF) | 0x07F80000; 
delay();
58
 }
 for(j=0xFF; j>0; j--)
 {
LPC_GPIO0->FIOPIN =(LPC_GPIO0->FIOPIN & 0xFF807FFF); 
LPC_GPIO1->FIOPIN = (LPC_GPIO1->FIOPIN & 0xF807FFFF); 
delay();
 }
}
 }
