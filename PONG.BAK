
Uses Crt, GVga, GMouse, Mysz, Graphics, Graph, Gif, Help;

Type
    Save =
    Record
          Szybkosc : Shortint;
          Trudnosc : String;
    End;

Const
     ESC = #27;
     ENTER = #13;
     DOL = #80;
     GORA = #72;

Procedure EnterKey;
Var
   Znak : Char;
Begin
     Repeat
           Znak:=ReadKey;
     Until Znak=#13;
End;

Function NumStr(S : Integer) : String;
Var
   Zm : String;
Begin
     Str(S,Zm);
     NumStr:=Zm;
End;

Procedure Init320x200(BGI : String);
Var
   Driver, Mode, TestDriver, ErrCode : Integer;
   X : Integer;
{$F+}
Function TestDetect : Integer;
Begin
     TestDetect := 0;
End;
{$F-}
Begin
     TestDriver := InstallUserDriver('SVGA256', @TestDetect);
     If GraphResult <> grOk then
     Begin
          Writeln(#7,'Blad! Nieposiadasz sterownika grafiki!');
          Halt(1);
     End;
     Driver := Detect;
     InitGraph(Driver, Mode, BGI);
     ErrCode := GraphResult;
     If ErrCode <> grOk then
     Begin
          Writeln(#7,'NIE POSIADASZ STEROWNIKA GRAFIKI SVGA256.BGI!!!');
          Writeln('Blad : ', ErrCode);
          Halt(1);
     End;
End;

Procedure Kursor(X, Y : Integer);
Begin
     SetColor(20);
     Circle(X,Y,5);
     SetColor(21);
     Circle(X,Y,4);
     SetColor(22);
     Circle(X,Y,3);
     SetColor(23);
     Circle(X,Y,2);
     SetColor(24);
     Circle(X,Y,1);
     SetColor(25);
     Circle(X-1,Y,5);
     SetColor(26);
     Circle(X-1,Y,4);
     SetColor(27);
     Circle(X-1,Y,3);
     SetColor(28);
     Circle(X-1,Y,2);
     SetColor(29);
     Circle(X-1,Y,1);
End;

Var
   Znak, Znak2 : Char;
   Y : Integer;
   P, P2, P3 : Pointer;
   Size, Size2, Size3, Size4 : Word;
   F : File of Save;
   D : Save;
   Nr : Shortint;

Procedure Player1_Prosty;

Procedure Punkty1(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(20 + Nr * 2,20);
     End;
End;

Procedure Punkty2(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(300 - Nr * 2,20);
     End;
End;

Var
   X1, Dl, Y1, Y2 : Integer;
   Px, Py, Stx, Sty : Integer;
   Punkty_P1, Punkty_P2 : Integer;
   Znak : Char;
   Font : TFont;
   P1, P2, P3 : Pointer;
   Size1, Size2, Size3 : Word;

Procedure SetZaw(Nr : Byte);
Begin
     If Nr=1 then
     begin
          Stx:=-1;
     end;
     If Nr=2 then
     begin
          Stx:=1;
     end;
End;

Begin
LoadGif('STOL.GIF');
Cls(1);
Y1:=80;
Y2:=80;
Px:=160;
Py:=100;
Randomize;
SetZaw(Random(2)+1);
Sty:=2;
Punkty_P1:=0;
Punkty_P2:=0;
Ekran.OutTextXY(20,20,1,2,15,NumStr(Punkty_P1));
Ekran.OutTextXY(278,20,1,2,15,NumStr(Punkty_P2));
LoadGif('STOL.GIF');
Size1:=ImageSize(Px,Py,Px+1,Py+1);
GetMem(P1,Size1);
Size2:=ImageSize(1,Y1,2,Y1+40);
GetMem(P2,Size2);
Size3:=ImageSize(317,Y2,318,Y2+40);
GetMem(P3,Size3);
Repeat
      SetColor(15);
      Rectangle(0,0,319,199);
      SetColor(15);
      Line(210,193,213,193);
      If (Px>318) or (Px<1) then Stx:=-Stx; Px:=Px+Stx;
      If (Py>198) or (Py<1) then Sty:=-Sty; Py:=Py+Sty;
      If (Px<1) then begin Punkty_P2:=Punkty_P2+1; end;
      If (Px>318) then begin Punkty_P1:=Punkty_P1+1; end;
      If (Px>280) and (Py<Y2-10) then Y2:=Y2-10;
      If (Px>280) and (Py>Y2) then Y2:=Y2+10;
      If Y2=-10 then Y2:=Y2+10;
      If Y2=170 then Y2:=Y2-10;
      GetImage(Px,Py,Px+1,Py+1,P1^);
      SetColor(0);
      Plot(Px,Py,1);
      Plot(Px+1,Py,1);
      Plot(Px,Py+1,1);
      Plot(Px+1,Py+1,1);
      GetImage(1,Y1,2,Y1+40,P2^);
      GetImage(317,Y2,318,Y2+40,P3^);
      SetColor(12);
      Line(1,Y1,1,Y1+40);
      Line(2,Y1,2,Y1+40);
      Line(317,Y2,317,Y2+40);
      Line(318,Y2,318,Y2+40);
      Punkty1(Punkty_P1);
      Punkty2(Punkty_P2);
      Delay(D.Szybkosc);
      PutImage(1,Y1,P2^,NormalPut);
      PutImage(317,Y2,P3^,NormalPut);
      PutImage(Px,Py,P1^,NormalPut);
      If KeyPressed then
      Begin
           Znak:=ReadKey;
           If Znak=Gora then Y1:=Y1-10;
           If Znak=Dol then Y1:=Y1+10;
           If Y1=-10 then Y1:=Y1+10;
           If Y1=170 then Y1:=Y1-10;
      End;
      If (Px>0) and (Px<2) and (Py>Y1) and (Py<Y1+40) then Stx:=-Stx;
      If (Px>317) and (Px<320) and (Py>Y2) and (Py<Y2+40) then Stx:=-Stx;
      If Punkty_P1=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 1 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 1 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
      If Punkty_P2=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 2 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 2 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
Until Znak=ESC;
LoadGif('MENU.GIF');
End;

Procedure Player1_Trudny;

Procedure Punkty1(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(20 + Nr * 2,20);
     End;
End;

Procedure Punkty2(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(300 - Nr * 2,20);
     End;
End;

Var
   X1, Dl, Y1, Y2 : Integer;
   Px, Py, Stx, Sty, Sty2 : Integer;
   Punkty_P1, Punkty_P2 : Integer;
   Znak : Char;
   Font : TFont;
   P1, P2, P3 : Pointer;
   Size1, Size2, Size3 : Word;
   Sy : Integer;

Procedure SetZaw(Nr : Byte);
Begin
     If Nr=1 then
     begin
          Stx:=-1;
     end;
     If Nr=2 then
     begin
          Stx:=1;
     end;
End;

Begin
LoadGif('STOL.GIF');
Cls(1);
Y1:=80;
Y2:=80;
Px:=160;
Py:=100;
Sy:=60;
Randomize;
SetZaw(Random(2)+1);
Sty:=2;
Punkty_P1:=0;
Punkty_P2:=0;
Ekran.OutTextXY(20,20,1,2,15,NumStr(Punkty_P1));
Ekran.OutTextXY(278,20,1,2,15,NumStr(Punkty_P2));
LoadGif('STOL.GIF');
Size1:=ImageSize(Px,Py,Px+1,Py+1);
GetMem(P1,Size1);
Size2:=ImageSize(1,Y1,2,Y1+40);
GetMem(P2,Size2);
Size3:=ImageSize(317,Y2,318,Y2+40);
GetMem(P3,Size3);
Repeat
      SetColor(15);
      Rectangle(0,0,319,199);
      SetColor(15);
      Line(210,193,213,193);
      If (Px>318) or (Px<1) then Stx:=-Stx; Px:=Px+Stx;
      If (Py>198) or (Py<1) then Sty:=-Sty; Py:=Py+Sty;
      If (Px<1) then begin Punkty_P2:=Punkty_P2+1; end;
      If (Px>318) then begin Punkty_P1:=Punkty_P1+1; end;
      If (Px>280) and (Py-10<Y2-10) then Y2:=Y2-10;
      If (Px>280) and (Py-10>Y2) then Y2:=Y2+10;
      If Y2=-10 then Y2:=Y2+10;
      If Y2=170 then Y2:=Y2-10;
      GetImage(Px,Py,Px+1,Py+1,P1^);
      SetColor(0);
      Plot(Px,Py,1);
      Plot(Px+1,Py,1);
      Plot(Px,Py+1,1);
      Plot(Px+1,Py+1,1);
      GetImage(1,Y1,2,Y1+40,P2^);
      GetImage(317,Y2,318,Y2+40,P3^);
      SetColor(12);
      Line(1,Y1,1,Y1+40);
      Line(2,Y1,2,Y1+40);
      Line(317,Y2,317,Y2+40);
      Line(318,Y2,318,Y2+40);
      Line(158,Sy,158,Sy+80);
      Line(159,Sy,159,Sy+80);
      Line(160,Sy,160,Sy+80);
      Punkty1(Punkty_P1);
      Punkty2(Punkty_P2);
      Delay(D.Szybkosc);
      PutImage(1,Y1,P2^,NormalPut);
      PutImage(317,Y2,P3^,NormalPut);
      PutImage(Px,Py,P1^,NormalPut);
      If KeyPressed then
      Begin
           Znak:=ReadKey;
           If Znak=Gora then Y1:=Y1-10;
           If Znak=Dol then Y1:=Y1+10;
           If Y1=-10 then Y1:=Y1+10;
           If Y1=170 then Y1:=Y1-10;
      End;
      If (Px>0) and (Px<2) and (Py>Y1) and (Py<Y1+40) then Stx:=-Stx;
      If (Px>317) and (Px<320) and (Py>Y2) and (Py<Y2+40) then Stx:=-Stx;
      If (Px>158) and (Px<160) and (Py>Sy) and (Py<Sy+80) then Stx:=-Stx;
      If Punkty_P1=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 1 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 1 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
      If Punkty_P2=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 2 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 2 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
Until Znak=ESC;
LoadGif('MENU.GIF');
End;

Procedure Player1_Trzeci;

Procedure Punkty1(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(20 + Nr * 2,20);
     End;
End;

Procedure Punkty2(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(300 - Nr * 2,20);
     End;
End;

Var
   X1, Dl, Y1, Y2 : Integer;
   Px, Py, Stx, Sty, Sty2 : Integer;
   Punkty_P1, Punkty_P2 : Integer;
   Znak : Char;
   Font : TFont;
   P1, P2, P3, P4 : Pointer;
   Size1, Size2, Size3, Size4 : Word;
   Sy : Integer;

Procedure SetZaw(Nr : Byte);
Begin
     If Nr=1 then
     begin
          Stx:=-1;
     end;
     If Nr=2 then
     begin
          Stx:=1;
     end;
End;

Begin
LoadGif('STOL.GIF');
Cls(1);
Y1:=80;
Y2:=80;
Px:=160;
Py:=100;
Sy:=60;
Randomize;
SetZaw(Random(2)+1);
Sty:=2;
Sty2:=2;
Punkty_P1:=0;
Punkty_P2:=0;
Ekran.OutTextXY(20,20,1,2,15,NumStr(Punkty_P1));
Ekran.OutTextXY(278,20,1,2,15,NumStr(Punkty_P2));
LoadGif('STOL.GIF');
Size1:=ImageSize(Px,Py,Px+1,Py+1);
GetMem(P1,Size1);
Size2:=ImageSize(1,Y1,2,Y1+40);
GetMem(P2,Size2);
Size3:=ImageSize(317,Y2,318,Y2+40);
GetMem(P3,Size3);
Size4:=ImageSize(158,Sy,160,Sy+80);
GetMem(P4,Size4);
Repeat
      SetColor(15);
      Rectangle(0,0,319,199);
      SetColor(15);
      Line(210,193,213,193);
      If (Px>318) or (Px<1) then Stx:=-Stx; Px:=Px+Stx;
      If (Py>198) or (Py<1) then Sty:=-Sty; Py:=Py+Sty;
      If (Sy>118) or (Sy<1) then Sty2:=-Sty2; Sy:=Sy+Sty2;
      If (Px<1) then begin Punkty_P2:=Punkty_P2+1; end;
      If (Px>318) then begin Punkty_P1:=Punkty_P1+1; end;
      If (Px>280) and (Py-10<Y2-10) then Y2:=Y2-10;
      If (Px>280) and (Py-10>Y2) then Y2:=Y2+10;
      If Y2=-10 then Y2:=Y2+10;
      If Y2=170 then Y2:=Y2-10;
      GetImage(Px,Py,Px+1,Py+1,P1^);
      SetColor(0);
      Plot(Px,Py,1);
      Plot(Px+1,Py,1);
      Plot(Px,Py+1,1);
      Plot(Px+1,Py+1,1);
      GetImage(1,Y1,2,Y1+40,P2^);
      GetImage(317,Y2,318,Y2+40,P3^);
      GetImage(158,Sy,160,Sy+80,P4^);
      SetColor(12);
      Line(1,Y1,1,Y1+40);
      Line(2,Y1,2,Y1+40);
      Line(317,Y2,317,Y2+40);
      Line(318,Y2,318,Y2+40);
      Line(158,Sy,158,Sy+80);
      Line(159,Sy,159,Sy+80);
      Line(160,Sy,160,Sy+80);
      Punkty1(Punkty_P1);
      Punkty2(Punkty_P2);
      Delay(D.Szybkosc);
      PutImage(1,Y1,P2^,NormalPut);
      PutImage(317,Y2,P3^,NormalPut);
      PutImage(158,Sy,P4^,NormalPut);
      PutImage(Px,Py,P1^,NormalPut);
      If KeyPressed then
      Begin
           Znak:=ReadKey;
           If Znak=Gora then Y1:=Y1-10;
           If Znak=Dol then Y1:=Y1+10;
           If Y1=-10 then Y1:=Y1+10;
           If Y1=170 then Y1:=Y1-10;
      End;
      If (Px>0) and (Px<2) and (Py>Y1) and (Py<Y1+40) then Stx:=-Stx;
      If (Px>317) and (Px<320) and (Py>Y2) and (Py<Y2+40) then Stx:=-Stx;
      If (Px>158) and (Px<160) and (Py>Sy) and (Py<Sy+80) then Stx:=-Stx;
      If Punkty_P1=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 1 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 1 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
      If Punkty_P2=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 2 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 2 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
Until Znak=ESC;
LoadGif('MENU.GIF');
End;

Procedure Player2_Prosty;

Procedure Punkty1(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(20 + Nr * 2,20);
     End;
End;

Procedure Punkty2(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(300 - Nr * 2,20);
     End;
End;

Var
   X1, Dl, Y1, Y2 : Integer;
   Px, Py, Stx, Sty : Integer;
   Punkty_P1, Punkty_P2 : Integer;
   Znak : Char;
   Font : TFont;
   P1, P2, P3 : Pointer;
   Size1, Size2, Size3 : Word;

Procedure SetZaw(Nr : Byte);
Begin
     If Nr=1 then
     begin
          Stx:=-1;
     end;
     If Nr=2 then
     begin
          Stx:=1;
     end;
End;

Begin
LoadGif('STOL.GIF');
Cls(1);
Y1:=80;
Y2:=80;
Px:=160;
Py:=100;
Randomize;
SetZaw(Random(2)+1);
Sty:=2;
Punkty_P1:=0;
Punkty_P2:=0;
Ekran.OutTextXY(20,20,1,2,15,NumStr(Punkty_P1));
Ekran.OutTextXY(278,20,1,2,15,NumStr(Punkty_P2));
LoadGif('STOL.GIF');
Ustaw_Kursor(315,Y2);
Granice_Y(0,170);
Size1:=ImageSize(Px,Py,Px+1,Py+1);
GetMem(P1,Size1);
Size2:=ImageSize(1,Y1,2,Y1+40);
GetMem(P2,Size2);
Size3:=ImageSize(317,Y2,318,Y2+40);
GetMem(P3,Size3);
Repeat
      SetColor(15);
      Rectangle(0,0,319,199);
      SetColor(15);
      Line(210,193,213,193);
      If (Px>318) or (Px<1) then Stx:=-Stx; Px:=Px+Stx;
      If (Py>198) or (Py<1) then Sty:=-Sty; Py:=Py+Sty;
      If (Px<1) then begin Punkty_P2:=Punkty_P2+1; end;
      If (Px>318) then begin Punkty_P1:=Punkty_P1+1; end;
      Pozycja_Kursora(X1,Y2,Dl);
      GetImage(Px,Py,Px+1,Py+1,P1^);
      SetColor(0);
      Plot(Px,Py,1);
      Plot(Px+1,Py,1);
      Plot(Px,Py+1,1);
      Plot(Px+1,Py+1,1);
      GetImage(1,Y1,2,Y1+40,P2^);
      GetImage(317,Y2,318,Y2+40,P3^);
      SetColor(12);
      Line(1,Y1,1,Y1+40);
      Line(2,Y1,2,Y1+40);
      Line(317,Y2,317,Y2+40);
      Line(318,Y2,318,Y2+40);
      Punkty1(Punkty_P1);
      Punkty2(Punkty_P2);
      Delay(D.Szybkosc);
      PutImage(1,Y1,P2^,NormalPut);
      PutImage(317,Y2,P3^,NormalPut);
      PutImage(Px,Py,P1^,NormalPut);
      If KeyPressed then
      Begin
           Znak:=ReadKey;
           If Znak=Gora then Y1:=Y1-10;
           If Znak=Dol then Y1:=Y1+10;
           If Y1=-10 then Y1:=Y1+10;
           If Y1=170 then Y1:=Y1-10;
      End;
      If (Px=0) and (Py>Y1) and (Py<Y1+40) then Stx:=-Stx;
      If (Px=320) and (Py>Y2) and (Py<Y2+40) then Stx:=-Stx;
      If Punkty_P1=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 1 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 1 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
      If Punkty_P2=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 2 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 2 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
Until Znak=ESC;
LoadGif('MENU.GIF');
End;

Procedure Player2_Trudny;

Procedure Punkty1(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(20 + Nr * 2,20);
     End;
End;

Procedure Punkty2(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(300 - Nr * 2,20);
     End;
End;

Var
   X1, Dl, Y1, Y2 : Integer;
   Px, Py, Stx, Sty : Integer;
   Punkty_P1, Punkty_P2 : Integer;
   Znak : Char;
   Font : TFont;
   P1, P2, P3, P4 : Pointer;
   Size1, Size2, Size3, Size4 : Word;
   Sy : Integer;

Procedure SetZaw(Nr : Byte);
Begin
     If Nr=1 then
     begin
          Stx:=-1;
     end;
     If Nr=2 then
     begin
          Stx:=1;
     end;
End;

Begin
LoadGif('STOL.GIF');
Cls(1);
Y1:=80;
Y2:=80;
Px:=160;
Py:=100;
Sy:=60;
Randomize;
SetZaw(Random(2)+1);
Sty:=2;
Punkty_P1:=0;
Punkty_P2:=0;
Ekran.OutTextXY(20,20,1,2,15,NumStr(Punkty_P1));
Ekran.OutTextXY(278,20,1,2,15,NumStr(Punkty_P2));
LoadGif('STOL.GIF');
Ustaw_Kursor(315,Y2);
Granice_Y(0,170);
Size1:=ImageSize(Px,Py,Px+1,Py+1);
GetMem(P1,Size1);
Size2:=ImageSize(1,Y1,2,Y1+40);
GetMem(P2,Size2);
Size3:=ImageSize(317,Y2,318,Y2+40);
GetMem(P3,Size3);
Repeat
      SetColor(15);
      Rectangle(0,0,319,199);
      SetColor(15);
      Line(210,193,213,193);
      If (Px>318) or (Px<1) then Stx:=-Stx; Px:=Px+Stx;
      If (Py>198) or (Py<1) then Sty:=-Sty; Py:=Py+Sty;
      If (Px<1) then begin Punkty_P2:=Punkty_P2+1; end;
      If (Px>318) then begin Punkty_P1:=Punkty_P1+1; end;
      Pozycja_Kursora(X1,Y2,Dl);
      GetImage(Px,Py,Px+1,Py+1,P1^);
      SetColor(0);
      Plot(Px,Py,1);
      Plot(Px+1,Py,1);
      Plot(Px,Py+1,1);
      Plot(Px+1,Py+1,1);
      GetImage(1,Y1,2,Y1+40,P2^);
      GetImage(317,Y2,318,Y2+40,P3^);
      SetColor(12);
      Line(1,Y1,1,Y1+40);
      Line(2,Y1,2,Y1+40);
      Line(317,Y2,317,Y2+40);
      Line(318,Y2,318,Y2+40);
      Line(158,Sy,158,Sy+80);
      Line(159,Sy,159,Sy+80);
      Line(160,Sy,160,Sy+80);
      Punkty1(Punkty_P1);
      Punkty2(Punkty_P2);
      Delay(D.Szybkosc);
      PutImage(1,Y1,P2^,NormalPut);
      PutImage(317,Y2,P3^,NormalPut);
      PutImage(Px,Py,P1^,NormalPut);
      If KeyPressed then
      Begin
           Znak:=ReadKey;
           If Znak=Gora then Y1:=Y1-10;
           If Znak=Dol then Y1:=Y1+10;
           If Y1=-10 then Y1:=Y1+10;
           If Y1=170 then Y1:=Y1-10;
      End;
      If (Px>0) and (Px<2) and (Py>Y1) and (Py<Y1+40) then Stx:=-Stx;
      If (Px>317) and (Px<320) and (Py>Y2) and (Py<Y2+40) then Stx:=-Stx;
      If (Px>158) and (Px<160) and (Py>Sy) and (Py<Sy+80) then Stx:=-Stx;
      If Punkty_P1=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 1 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 1 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
      If Punkty_P2=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 2 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 2 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
Until Znak=ESC;
LoadGif('MENU.GIF');
End;

Procedure Player2_Trzeci;

Procedure Punkty1(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(20 + Nr * 2,20);
     End;
End;

Procedure Punkty2(Nr : Byte);
Procedure Kreska(X, Y : Integer);
Begin
     SetColor(20);
     Line(X,Y,X,Y+10);
End;
Begin
     If Nr=0 then
     Begin
     End;
     If Nr>0 then
     Begin
          Kreska(300 - Nr * 2,20);
     End;
End;

Var
   X1, Dl, Y1, Y2 : Integer;
   Px, Py, Stx, Sty, Sty2 : Integer;
   Punkty_P1, Punkty_P2 : Integer;
   Znak : Char;
   Font : TFont;
   P1, P2, P3, P4 : Pointer;
   Size1, Size2, Size3, Size4 : Word;
   Sy : Integer;

Procedure SetZaw(Nr : Byte);
Begin
     If Nr=1 then
     begin
          Stx:=-1;
     end;
     If Nr=2 then
     begin
          Stx:=1;
     end;
End;

Begin
LoadGif('STOL.GIF');
Cls(1);
Y1:=80;
Y2:=80;
Px:=160;
Py:=100;
Sy:=60;
Randomize;
SetZaw(Random(2)+1);
Sty:=2;
Sty2:=2;
Punkty_P1:=0;
Punkty_P2:=0;
Ekran.OutTextXY(20,20,1,2,15,NumStr(Punkty_P1));
Ekran.OutTextXY(278,20,1,2,15,NumStr(Punkty_P2));
LoadGif('STOL.GIF');
Ustaw_Kursor(315,Y2);
Granice_Y(0,170);
Size1:=ImageSize(Px,Py,Px+1,Py+1);
GetMem(P1,Size1);
Size2:=ImageSize(1,Y1,2,Y1+40);
GetMem(P2,Size2);
Size3:=ImageSize(317,Y2,318,Y2+40);
GetMem(P3,Size3);
Size4:=ImageSize(158,Sy,160,Sy+80);
GetMem(P4,Size4);
Repeat
      SetColor(15);
      Rectangle(0,0,319,199);
      SetColor(15);
      Line(210,193,213,193);
      If (Px>318) or (Px<1) then Stx:=-Stx; Px:=Px+Stx;
      If (Py>198) or (Py<1) then Sty:=-Sty; Py:=Py+Sty;
      If (Sy>118) or (Sy<1) then Sty2:=-Sty2; Sy:=Sy+Sty2;
      If (Px<1) then begin Punkty_P2:=Punkty_P2+1; end;
      If (Px>318) then begin Punkty_P1:=Punkty_P1+1; end;
      Pozycja_Kursora(X1,Y2,Dl);
      GetImage(Px,Py,Px+1,Py+1,P1^);
      SetColor(0);
      Plot(Px,Py,1);
      Plot(Px+1,Py,1);
      Plot(Px,Py+1,1);
      Plot(Px+1,Py+1,1);
      GetImage(1,Y1,2,Y1+40,P2^);
      GetImage(317,Y2,318,Y2+40,P3^);
      GetImage(158,Sy,160,Sy+80,P4^);
      SetColor(12);
      Line(1,Y1,1,Y1+40);
      Line(2,Y1,2,Y1+40);
      Line(317,Y2,317,Y2+40);
      Line(318,Y2,318,Y2+40);
      Line(158,Sy,158,Sy+80);
      Line(159,Sy,159,Sy+80);
      Line(160,Sy,160,Sy+80);
      Punkty1(Punkty_P1);
      Punkty2(Punkty_P2);
      Delay(D.Szybkosc);
      PutImage(1,Y1,P2^,NormalPut);
      PutImage(317,Y2,P3^,NormalPut);
      PutImage(158,Sy,P4^,NormalPut);
      PutImage(Px,Py,P1^,NormalPut);
      If KeyPressed then
      Begin
           Znak:=ReadKey;
           If Znak=Gora then Y1:=Y1-10;
           If Znak=Dol then Y1:=Y1+10;
           If Y1=-10 then Y1:=Y1+10;
           If Y1=170 then Y1:=Y1-10;
      End;
      If (Px>0) and (Px<2) and (Py>Y1) and (Py<Y1+40) then Stx:=-Stx;
      If (Px>317) and (Px<320) and (Py>Y2) and (Py<Y2+40) then Stx:=-Stx;
      If (Px>158) and (Px<160) and (Py>Sy) and (Py<Sy+80) then Stx:=-Stx;
      If Punkty_P1=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 1 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 1 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
      If Punkty_P2=10 then
      begin
          SetColor(12);
          Line(1,Y1,1,Y1+40);
          Line(2,Y1,2,Y1+40);
          Line(317,Y2,317,Y2+40);
          Line(318,Y2,318,Y2+40);
          Ekran.OutTextXY(50,93,2,2,7,'PLAYER 2 WIN');
          Ekran.OutTextXY(50,94,2,2,8,'PLAYER 2 WIN');
          EnterKey;
          Znak:=ESC;
          LoadGif('MENU.GIF');
      end;
Until Znak=ESC;
LoadGif('MENU.GIF');
End;

Var
   Image : TImage;

Procedure Start;
Var
   X : Integer;
Begin
     TextBackground(0);
     TextColor(0);
     ClrScr;
     For X:=1 to 80 do
     Begin
          GotoXY(X,1);
          TextColor(1);
          Write('Û');
     End;
     TextBackground(1);
     PiszDivX(1,15,'MENU START PONG 2000 ver. 2.0 FREEWARE');
     TextBackground(0);
     PiszXY(2,3,15,'PONG 2000 ver. 2.0 FREEWARE : FULL VERSION');
     PiszXY(2,5,15,'SPRAWDZANIE PLIKOW :');
     PiszXY(2,7,15,'PONG.CFG - ');
     TextColor(12);
     CzyPlikIstnieje('PONG.CFG','Ok','Brak!');
     PiszXY(2,8,15,'INFO.GIF - ');
     TextColor(12);
     CzyPlikIstnieje('INFO.GIF','Ok','Brak!');
     PiszXY(2,9,15,'MENU.GIF - ');
     TextColor(12);
     CzyPlikIstnieje('MENU.GIF','Ok','Brak!');
     TextColor(12);
     PiszXY(2,10,15,'OPCJE.GIF - ');
     TextColor(12);
     CzyPlikIstnieje('OPCJE.GIF','Ok','Brak!');
     TextColor(12);
     PiszXY(2,11,15,'STOL.GIF - ');
     TextColor(12);
     CzyPlikIstnieje('STOL.GIF','Ok','Brak!');
     PiszXY(2,12,15,'SVGA256.BGI - ');
     TextColor(12);
     CzyPlikIstnieje('SVGA256.BGI','Ok','Brak!');
     WriteLn;
     TextColor(15);
     If MouseExist Then PiszXY(2,13,15,'Mysz - ')
     Else
     Begin
          TextColor(12);
          Write('Brak!');
          Halt;
     End;
     TextColor(12);
     Write('Ok');
     PiszXY(2,15,15,'ENTER...');
     EnterKey;
End;

Begin
Start;
Init320x200('');
D.Szybkosc:=20;
D.Trudnosc:='PROSTY';
Assign(F,'PONG.CFG');
Reset(F);
Read(F,D);
Close(F);
If D.Trudnosc='PROSTY' then Nr:=1;
If D.Trudnosc='TRUDNY' then Nr:=2;
If D.Trudnosc='??????' then Nr:=3;
LoadGif('MENU.GIF');
Y:=62;
Size:=ImageSize(94,Y-5,225,Y+5);
GetMem(P,Size);
Repeat
      GetImage(94,Y-5,225,Y+5,P^);
      Kursor(100,Y);
      Kursor(220,Y);
      Znak:=ReadKey;
      PutImage(94,Y-5,P^,NormalPut);
      If Znak=Gora then Y:=Y-27;
      If Znak=Dol then Y:=Y+27;
      If Y=35 then Y:=Y+27; {GRANICE GORA}
      If Y=197 then Y:=Y-27; {GRANICE DOL}
      If (Y=62) and (Znak=ENTER) then {PLAYER 1}
      Begin
           If D.Trudnosc='PROSTY' then
           Begin
                Player1_Prosty;
                FreeImage(Image);
           End;
           If D.Trudnosc='TRUDNY' then
           Begin
                Player1_Trudny;
                FreeImage(Image);
           End;
           If D.Trudnosc='??????' then
           Begin
                Player1_Trzeci;
                FreeImage(Image);
           End;
           Y:=62;
      End;
      If (Y=89) and (Znak=ENTER) then {PLAYER 2}
      Begin
           If D.Trudnosc='PROSTY' then
           Begin
                Player2_Prosty;
                FreeImage(Image);
           End;
           If D.Trudnosc='TRUDNY' then
           Begin
                Player2_Trudny;
                FreeImage(Image);
           End;
           If D.Trudnosc='??????' then
           Begin
                Player2_Trzeci;
                FreeImage(Image);
           End;
           Y:=89;
      End;
      If (Y=116) and (Znak=ENTER) then {OPCJE}
      Begin
           LoadGif('OPCJE.GIF');
           Y:=97;
           Size2:=ImageSize(294,Y-5,305,Y+5);
           Size3:=ImageSize(130,90,190,115);
           Size4:=ImageSize(130,118,222,132);
           GetMem(P,Size2);
           GetMem(P2,Size3);
           GetMem(P3,Size4);
           Repeat
                 SetColor(100);
                 SetTextStyle(0,0,2);
                 GetImage(130,90,190,115,P2^);
                 GetImage(130,118,222,132,P3^);
                 OutTextXY(130,92,NumStr(D.Szybkosc));
                 OutTextXY(130,119,D.Trudnosc);
                 GetImage(294,Y-5,305,Y+5,P^);
                 Kursor(300,Y);
                 Znak2:=ReadKey;
                 PutImage(294,Y-5,P^,NormalPut);
                 PutImage(130,90,P2^,NormalPut);
                 PutImage(130,118,P3^,NormalPut);
                 If Znak2=GORA then Y:=Y-27;
                 If Znak2=DOL then Y:=Y+27;
                 If Y=70 then Y:=Y+27;
                 If Y=205 then Y:=Y-27;
                 If (Y=97) and (Znak2='+') then D.Szybkosc:=D.Szybkosc+1;
                 If (Y=97) and (Znak2='-') then D.Szybkosc:=D.Szybkosc-1;
                 If (Y=124) and (Znak2=ENTER) then Nr:=Nr+1;
                 If (Nr=1) then
                 begin
                      D.Trudnosc:='PROSTY';
                 end;
                 If (Nr=2) then
                 begin
                      D.Trudnosc:='TRUDNY';
                 end;
                 If (Nr=3) then
                 begin
                      D.Trudnosc:='??????';
                 end;
                 If Nr=3 then Nr:=0;
                 If D.Szybkosc=100 then D.Szybkosc:=D.Szybkosc-1;
                 If D.Szybkosc=-1 then D.Szybkosc:=D.Szybkosc+1;
                 If (Y=151) and (Znak2=ENTER) then
                 begin
                      Assign(F,'PONG.CFG');
                      Rewrite(F);
                      Write(F,D);
                      Close(F);
                 end;
           Until (Y=178) and (Znak2=ENTER);
           Y:=116;
           FreeImage(Image);
           LoadGif('MENU.GIF');
      End;
      If (Y=143) and (Znak=ENTER) then {INFO}
      Begin
           LoadGif('INFO.GIF');
           Repeat
                 Znak2:=ReadKey;
           Until Znak2=ENTER;
           Y:=143;
           FreeImage(Image);
           LoadGif('MENU.GIF');
      End;
      If (Y=170) and (Znak=ENTER) then {WYJSCIE}
      Begin
           TextMode(co80);
           TextBackground(0);
           TextColor(7);
           TextColor(14);
           WriteLn(' Copyright (c) 2000');
           WriteLn('   F R E E W A R E');
           WriteLn(' by MICHAL RYGIELSKI');
           WriteLn('POLAND (056) 648-03-72');
           Halt;
           FreeImage(Image);
      End;
Until Znak='PONG Copyright (c) 2000 FREEWARE by MICHAL RYGIELSKI';
CloseGraph;
TextMode(co80);
End.