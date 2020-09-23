<div align="center">

## Parabola Graphing Machine


</div>

### Description

Enter a parabola in the form of y = ax^2 + bx + c. Then the program will graph the parabola and give you info about the parabola. Very simple and easy to follow code. Please comment and vote.
 
### More Info
 
There is a specific range for the parabola which you will see once you run the program.

No side effects.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Dario S\.](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/dario-s.md)
**Level**          |Intermediate
**User Rating**    |5.0 (15 globes from 3 users)
**Compatibility**  |C, C\+\+ \(general\), Borland C\+\+
**Category**       |[Math](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/math__3-12.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/dario-s-parabola-graphing-machine__3-3126/archive/master.zip)

### API Declarations

```
I don't know which ones you actually need and which ones you don't.
#include <vcl.h>
#include <condefs.h>
#include <time.h>
#include <stdio.h>
#include <iostream.h>
#include <conio.h>
#include <dos.h>
#include <stdlib.h>
#include <fstream.h>
```


### Source Code

```
//parabolas Ax^2 + Bx + C = y
#include <vcl.h>
#include <condefs.h>
#include <time.h>
#include <stdio.h>
#include <iostream.h>
#include <conio.h>
#include <dos.h>
#include <stdlib.h>
#include <fstream.h>
#pragma hdrstop
#pragma argused
void enter_values(void);
void find_vertex(void);
void find_other_points(void);
void draw_axis(void);
void print_point(void);
bool check_point(int counter);
float a, b, c;
float x, y;
float vertex[2];
float coordinates[72][2];
int  graph_coor[13][2];
float scale[2] = {2, 0};
int main()
 {
 int counter;
 char cuadrado = 0xFD;
 enter_values();
 find_vertex();
 find_other_points();
 draw_axis();
 print_point();
 getch();
 clrscr();
 cout << "y = " << a << "x" << cuadrado << " ";
 if(b >= 0)
  {cout << "+ ";}
 cout << b << "x ";
 if(c >= 0)
  {cout << "+ ";}
 cout << c << endl << endl;
 cout << "y = " << a << "(x ";
 if(vertex[0] >= 0)
  {cout << " - " << vertex[0];}
 else
  {cout << " + " << -1*vertex[0];}
 cout << ")" << cuadrado << " ";
 if(vertex[1] >= 0)
  {cout << "+ ";}
 cout << vertex[1] << endl << endl;
 cout << "VERTEX (" << vertex[0] << ", " << vertex[1] << ") " << endl << endl;
 cout << "Table of values" << endl;
 cout << "^^^^^ ^^ ^^^^^^" << endl << endl;
 for(counter = 30; counter < 43; counter++)
   {
   cout << "(" << coordinates[counter][0] << ", " << coordinates[counter][1] << ") " << endl;
   }
 getch();
 return 0;
 }
void enter_values(void)
 {
 clrscr();
 cprintf("y = Ax%c + Bx + C \r\n", 0xFD);
 cout << "Enter a value for 'A': ";
 cin >> a;
 cout << "Enter a value for 'B': ";
 cin >> b;
 cout << "Enter a value for 'C': ";
 cin >> c;
 }
void find_vertex(void)
 {
 //y = x^2 + B/Ax + C/A
 if(a != 0)
  {vertex[0] = b/a/2*-1;}
 vertex[1] = a*(vertex[0]*vertex[0]) + b*vertex[0] + c;
 }
void find_other_points(void)
 {
 int counter;
 float counter_copy;
 float x_coor;
 x_coor = vertex[0] - 18;
 for(counter = 0; counter < 72; counter++)
   {
   counter_copy = counter;
   coordinates[counter][0] = x_coor + counter_copy/2;
   coordinates[counter][1] = a*(coordinates[counter][0]*coordinates[counter][0]) + b*coordinates[counter][0] + c;
   }
 }
void draw_axis(void)
 {
 clrscr();
 int counter_x, counter_y, counter;
 for(counter = 1; counter < 80; counter++)
   {gotoxy(counter, 13);cprintf("%c", 0xC4);}
 for(counter = 1; counter < 25; counter++)
   {gotoxy(40, counter); cprintf("%c", 0xB3);}
 for(counter = 2; counter < 40; counter+=2)
   {
   if(counter-20 != 0)
    {
    gotoxy(counter*2, 14); cprintf("%d", counter-20);
    gotoxy(counter*2, 13); cprintf("%c", 0xC2);
    }
   }
 for(counter = 1; counter < 24; counter+=2)
   {
   if(13-counter != 12 && 13-counter != 0)
    {
    gotoxy(40, counter);
    cprintf("%c%d", 0xC3, 13-counter);
    }
   }
 gotoxy(1, 13); cprintf("%c", 0x1B);
 gotoxy(1, 14); cprintf("x");
 gotoxy(40, 1); cprintf("%cy", 0x18);
 gotoxy(40, 24); cprintf("%c", 0x19);
 gotoxy(79, 13); cprintf("%c", 0x1A);
 gotoxy(40, 13); cprintf("%c", 0xC5);
 }
void print_point(void)
 {
 int counter;
 int coor[2];
 int add;
 int counter2;
 for(counter = 0; counter < 80; counter++)
   {if(counter == vertex[0])
    {counter2 = 0;}
   }
 for(counter = 0; counter < 72; counter++)
   {
   if(check_point(counter) == true)
    {
    textcolor(RED);
    coor[0] = 40+coordinates[counter][0]*2;
    coor[1] = 13-coordinates[counter][1];
    gotoxy(coor[0], coor[1]);
    cprintf("%c", 0x04);
    }
   counter2++;
   }
 textcolor(WHITE);
 }
bool check_point(int counter)
 {
 if(40+coordinates[counter][0]*2 > 79 || 40+coordinates[counter][0]*2 < 1)
  {return false;}
 if(13-coordinates[counter][1] < 1 || 13-coordinates[counter][1] > 24)
  {return false;}
 return true;
 }
```

