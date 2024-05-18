# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS
# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

# APPARATUS REQUIRED:
   Xilinx 14.7  Spartan6 FPGA                                                                                                                                                                                                                                                                                                                                                                                                 
                                                                                                                                                                                            
# PROCEDURE
```
STEP:1  Start  the Xilinx navigator, Select and Name the New project.
STEP:2  Select the device family, device, package and speed.       
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.
```

# LOGIC DIAGRAM:
# SR FLIPFLOP:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)

# VERILOG CODE
```
module SRflipflop(clk,rst,s,r,q);
input clk,rst,s,r;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bx;
endcase
end 
end
endmodule
```

# OUTPUT

![Screenshorts Image 2024-04-13 at 10 00 01_cccc0e6e](https://github.com/Mohanraj7896/VLSI-LAB-EXP-4/assets/166592482/1521f019-5a03-4ac5-aba5-e803e73d033c)


# LOGIC DIAGRAM:
# JK FLIPFLOP:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

# VERILOG CODE
```
module JKflipflop(clk,rst,s,r,q);
input clk,rst,s,r;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=1;
2'b11:q=~q;
endcase
end 
end
endmodule
```

# OUTPUT

![Screenshot 2024-04-06 111138](https://github.com/Mohanraj7896/VLSI-LAB-EXP-4/assets/166592482/ba74630c-893b-4c8e-be63-86afd5b936bf)

# LOGIC DIAGRAM:
# T FLIPFLOP:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)

# VERILOG CODE
```
module tff(clk,rst,j,q);
input clk,rst,j;
output reg q;
always@(posedge clk)
begin
case(t)
1'b0:q=q;
1'b1:q=~q;
default=q=1'b0;
endcase
end
endmodule
```

# OUTPUT

![Screenshorts Image 2024-04-13 at 10 00 01_b6dbd5ed](https://github.com/Mohanraj7896/VLSI-LAB-EXP-4/assets/166592482/a5052c21-91f8-4279-919d-e0a2313b175d)

# LOGIC DIAGRAM
# D FLIPFLOP:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)

```
module Dflipflop(clk,d,rst,out);
input clk,d,rst;
output reg out;
always@(posedge clk)
begin
if(rst==1)
out = 1'b0;
else
out = d;
end 
endmodule
```

# OUTPUT

![Screenshorts Image 2024-04-13 at 09 59 59_756c502c](https://github.com/Mohanraj7896/VLSI-LAB-EXP-4/assets/166592482/6135817b-ca0f-40f3-b875-ebfeeb6e1ecd)

# LOGIC DIAGRAM
# RIPPLECARRY COUNTER:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)

# VERILOG CODE
```
module ripplecounter(q,clk,reset);
input clk,reset;
output[3:0]q;
T_FF tff0(q[0],clk,reset);
T_FF tff1(q[1],q[0],reset);
T_FF tff2(q[2],q[1],reset);
T_FF tff3(q[3],q[2],reset);
endmodule
module D_FF(q,d,clk,reset);
input d,clk,reset;
output reg q;
always@(negedge clk or posedge reset)
begin
if(reset)
q<=1'b0;
else
q<=d;
end
endmodule
module T_FF(q,clk,reset);
input clk,reset;
output q;
wire d;
D_FF dff0(q,d,clk,reset);
not n1(d,q);
endmodule
```
# OUTPUT

![Screenshorts Image 2024-04-13 at 10 00 01_3d4faf78](https://github.com/Mohanraj7896/VLSI-LAB-EXP-4/assets/166592482/9667d293-d980-4c8f-bd09-2bc8dcbd3636)

# UPDOWN COUNTER
# VERILOG CODE
```
module updowncounter(clk,rest,a,counter);
input clk,rest,a;
output [3:0]counter;
reg [3:0]counter;
always@(posedge clk)
begin
if(rest)
counter=4'b0;
else
begin
if(a==1)
counter=counter+4'b1;
else
counter=counter-4'b1;
end
end
endmodul
```

# OUTPUT

![Screenshorts Image 2024-04-13 at 10 00 02_830c6fca](https://github.com/Mohanraj7896/VLSI-LAB-EXP-4/assets/166592482/d05773a7-cff0-4e28-aaad-c682fd0b1563)

# MOD 10 COUNTER
```
module modcounter(reset,clk,counter);
input reset,clk;
output [3:0]counter;
reg [3:0]counter;
always@(posedge clk)
begin
    if(reset)
        counter<= 4'b0;
     else
         counter<= counter+1;
 end
endmodule
```

# OUTPUT![Screenshorts Image 2024-04-13 at 10 00 01_ffae364b](https://github.com/Mohanraj7896/VLSI-LAB-EXP-4/assets/166592482/03bb71fa-c95c-463f-86f3-317b3999efc9)

# RESULT
Hence The simulation and synthesis of SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023 is done and output verified successfully.
