# VLSI-LAB-EXP-4
SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOPS, COUNTERS design using vivado.

# APPARATUS REQUIRED: 

vivado 2023.2

# PROCEDURE

STEP:1 Start the vivado software, Select and Name the New project.

STEP:2 Select the device family, device, package and speed.

STEP:3 Select new source in the New Project and select Verilog Module as the Source type.

STEP:4 Type the File Name and module name and Click Next and then finish button. Type the code and save it.

STEP:5 Select the run simulation and then run Behavioral Simulation in the Source Window and click the check syntax.

STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table.

STEP:7 compare the output with truth table.

# SR FLIPFLOP

LOGIC DIAGRAM:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)

VERILOG CODE:

module srff(clk,j,k,rst,q );

input s,r,clk,rst;

output reg q;

always@(posedge clk)

begin

if(rst==1)

q=1'b0;

else

begin

case({s,r})

2'b00: q=q;

2'b01:q=1'b0;

2'b10:q=1'b1;

2'b11:q=1'bx;

endcase

end

end

endmodule

OUTPUT:


![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/7d971694-c833-4640-b3ae-072ecdda9f08)


# JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

VERILOG CODE:

module jkff(clk,j,k,rst,q );

input j,k,clk,rst;

output reg q;

always@(posedge clk)

begin

if(rst==1)

q=1'b0;

else

begin

case({j,k})

2'b00: q=q;

2'b01:q=1'b0;

2'b10:q=1'b1;

2'b11:q=~q;

endcase

end

end

endmodule

OUTPUT:

![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/f45a459a-6a9c-4897-b68f-af15d59e3dc4)


# T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)

VERILOG CODE:

module tff(clk,reset,t,q);

input clk,reset,t;

output reg q;

always @(posedge clk)

begin

if(reset==1)

q=0;

else

begin

if(t==0)

q=q;

else

q=~q;

end

end

endmodule

OUTPUT:

![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/45c67dad-daab-438d-8521-fcae4ab7715f)


# D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)

VERILOG CODE:

module dff(clk,d,rst,q );

input d,clk,rst;

output reg q;

always@(posedge clk)

begin

if(rst==1)

q=1'b0;

else

q=d;

end

endmodule

OUTPUT:

![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/ebdaa696-2e66-474b-b426-b7b4b5e6d550)


# UPDOWNCOUNTER: 

CIRCUITDIAGRAM: 

![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/fd0932c4-bc65-424b-a082-788f62c9fc29)

TRUTH TABLE:

![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/eb77495e-3ed7-4291-a8fc-d2e2fd3baeb3)

VERILOG CODE:

module updown(clk,rst,up_down,count);

input clk,rst,up_down;

output reg[3:0]count;

always@(posedge clk)

begin

if(rst==1)

count <= 4'b0000;

else if (up_down == 1'b1)

count <= count + 1'b1;

else

count <= count-1'b1;

end

endmodule

OUTPUT:

![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/3d77d5df-2f7e-49a9-bed8-4667c2f7b4b5)

# MOD 10 COUNTER:

CIRCUIT DIAGRAM:

![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/dd1e30aa-1632-43a7-b222-e6dc763e3fcf)

VERILOG CODE

module mod(clk,rst,count);

input  clk,rst;

output reg[3:0]count;

always @(posedge clk)

begin

if(rst==1 | count==4'b1001)

count <= 4'b0000;

else

count <= count +1;  

end

endmodule

OUTPUT:

![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/eb64718d-bba0-4396-98a5-1d4a2a6358c9)

# RIPPLE COUNTER:

LOGIC DIAGRAM


![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/f9c1d219-3923-467c-b1fa-ce2627e55035)


![image](https://github.com/teja2134/VLSI-LAB-EXP-4/assets/161149578/3a2a7efb-8b44-4015-ab32-f59ac52c2142)


VERILOG CODE:

module ripplecounter(clk,rst,q);

input clk,rst;

output [3:0]q;

tff tff1(q[0],clk,rst);

tff tff2(q[1],q[0],rst);

tff tff3(q[2],q[1],rst);

tff tff4(q[3],q[2],rst);

endmodule

module tff(q,clk,rst);

input clk,rst;

output q;

wire d;

dff df1(q,d,clk,rst);

not n1(d,q);

endmodule

module dff(q,d,clk,rst);

input d,clk,rst;

output q;

reg q;

always@(posedge clk or posedge rst)

begin

if(rst)

   q=1'b10;

else

   q=d;

end

endmodule


OUTPUT:


![Uploading image.png…]()


![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)



# RESULT

   Thus,the simulation and synthesis of SR,JK,T,D flipflops,counters by using vivado has been successfully excecuted and verified.

