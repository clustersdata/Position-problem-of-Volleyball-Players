# Position-problem-of-Volleyball-Players

Position problem of Volleyball Players

图为排球场的平面图，其中一、二、三、四、五、六为位置编号，

┃　　　　　　　　┃二、三、四号位置为前排，一、六、五号位为后排。某队比赛时，

┃　　　　　　　　┃一、四号位放主攻手，二、五号位放二传手，三、六号位放副攻

┠──┬──┬──┨手。队员所穿球衣分别为１，２，３，４，５，６号，但每个队

┃ 四 │ 三 │ 二 ┃员的球衣都与他们的站位号不同。已知１号、６号队员不在后排，

┠──┼──┼──┨２号、３号队员不是二传手，３号、４号队员不在同一排，５号、

┃ 五 │ 六 │ 一 ┃６号队员不是副攻手。

┗━━┷━━┷━━┛	编程求每个队员的站位情况。

【算法分析】本题可用一般的穷举法得出答案。也可用回溯法。以下为回溯解法。

【参考程序】

type sset=set of 1..6;

var   a:array[1..6]of 1..6;

      d:array[1..6]of sset;
      
      i:integer;
      
procedure output; {输出}

begin

	       if not( (a[3]in [2,3,4])= (a[4] in[2,3,4])) then
         
	       begin				 { 3,4号队员不在同一排 }
         
		  write('number:');for i:=1 to 6 do write(i:8);writeln;
      
		  write('weizhi:');for i:=1 to 6 do write(a[i]:8);writeln;
      
	       end;
         
end;


procedure try(i:integer;s:sset); {递归过程  i:第i个人,s:哪些位置已安排人了}

var

   j,k:integer;
   
begin

     for j:=1 to 6 do begin	{每个人都有可能站1-6这6个位置}
     
	   if (j in d[i]) and not(j in s) then begin
     
	     {j不在d[i]中,则表明第i号人不能站j位. j如在s集合中,表明j位已排人了}
       
	      a[i]:=j;		   {第 i 人可以站 j 位}
        
	      if i<6 then try(i+1,s+[j])   {未安排妥,则继续排下去}
        
		     else  output;	   {6个人都安排完,则输出}
         
	    end;
      
       end;
       
end;

begin

     for i:=1 to 6 do d[i]:=[1..6]-[i];       {每个人的站位都与球衣的号码不同}
     
     d[1]:=d[1]-[1,5,6];
     
     d[6]:=d[6]-[1,5,6];     {1,6号队员不在后排}
     
     d[2]:=d[2]-[2,5];
     
     d[3]:=d[3]-[2,5];	     {2,3号队员不是二传手}
     
     d[5]:=d[5]-[3,6];
     
     d[6]:=d[6]-[3,6];	     {5,6号队员不是副攻手}
     
     try(1,[]);
     
end.

