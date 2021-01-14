# finalproject_14
* 8x8 LED矩陣 用來顯示遊戲畫面

![image](https://github.com/chloe0919/finalproject_14/blob/main/S__7856138.jpg)

* 七段顯示器 顯示遊戲的時間

![image](https://github.com/chloe0919/finalproject_14/blob/main/S__7856134.jpg)

* LED陣列 顯示血量跟計分

![image](https://github.com/chloe0919/finalproject_14/blob/main/S__7856132.jpg)

* 4bits SW按鈕 左到右為Clear->Left->right

![image](https://github.com/chloe0919/finalproject_14/blob/main/S__7856139.jpg)

* 贏的畫面

![image](https://github.com/chloe0919/finalproject_14/blob/main/S__7856136.jpg)

* 輸的畫面

![image](https://github.com/chloe0919/finalproject_14/blob/main/S__7856137.jpg)

遊玩方式:
-------

掉落物分綠色和藍色 若碰到綠色 紅色血量會扣一 碰到藍色 紅色血量加一
分數計算總共碰到藍色的次數 若達到五次 就會顯示贏的畫面 若血量扣完則顯示輸的畫面

程式模組說明:
------- 

module LD_final_project(output reg [7:0] DATA_R, DATA_G, DATA_B,          //8X8 LED矩陣顏色
								output reg [6:0] d7_1,                                   //七段顯示器
								output reg [2:0] COMM, Life,                             //COMM:控制8X8LED亮,Life:顯示血量
								output reg [4:0] Light,                                  //顯示分數
								output reg [1:0] COMM_CLK,                               //控制七段顯示器亮
								output EN,                                               //8X8矩陣的控制訊號燈
								input CLK, clear, Left, Right);                          
	reg [7:0] plate [7:0];                                                 //綠色掉落物
	reg [7:0] people [7:0];                                                //紅色移動人物
	reg [7:0] bonus [7:0];                                                 //藍色掉落物
	reg [6:0] seg1, seg2;                                                  //七段顯示器
	reg [3:0] bcd_s,bcd_m;                                                 //用來計算分秒
	reg [2:0] random01, random02, random03,random04, r, r1, r2,r3;         //用來產生亂數決定掉落物位置
	reg left, right, temp;
	segment7 S0(bcd_s, A0,B0,C0,D0,E0,F0,G0);                              //秒數轉7段顯示器
	segment7 S1(bcd_m, A1,B1,C1,D1,E1,F1,G1);
	divfreq div0(CLK, CLK_div);                                            //視覺暫留除頻器
	divfreq1 div1(CLK, CLK_time);                                          //計時除頻器
	divfreq2 div2(CLK, CLK_mv);                                            //掉落物&人物移動除頻器
	byte line, count, count1;                                              
	integer a, b, c,d, touch,grade;                                        //touch:碰到綠色次數,grade:碰到藍色次數

Demo影片展示:
---------

[![Watch the video](https://i.imgur.com/vKb2F1B.png)](https://drive.google.com/drive/u/2/my-drive)
