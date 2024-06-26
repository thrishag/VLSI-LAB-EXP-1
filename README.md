# VLSI-LAB-EXPERIMENTS
AIM:  
    
To simulate and synthesis Logic Gates,Adders and Subtractor using Xilinx ISE.

APPARATUS REQUIRED:  

vivado 2023.2

PROCEDURE: 


STEP:1  Start the Xilinx navigator, Select and Name the New project. 


STEP:2  Select the device family, device, package and speed. 


STEP:3  Select new source in the New Project and select Verilog Module as the Source type. 


STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it. 


STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.


STEP:6  Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table. 


STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window. 


STEP:8  Select Check Syntax from the Synthesize XST Process. Double Click in the Floorplan Area/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 



STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu. 



STEP:10  Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here. 



STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.



STEP:12  Load the Bit file into the SPARTAN 6 FPGA


Logic Diagram :

Logic Gates:



![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/ee17970c-3ac9-4603-881b-88e2825f41a4)



Half Adder:



![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/0e1ecb96-0c25-4556-832b-aeeedfdfe7b9)



Full adder:



![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/9bb3964c-438f-469d-a3de-c1cca6f323fb)



Half Subtractor:



![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/731470b7-eb4e-49f8-8bb7-2994052a7184)




Full Subtractor:



![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/d66f874b-c1f2-44b3-a035-7149b56430c1)



8 Bit Ripple Carry Adder



![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/7385a408-40a5-4203-8050-b72818622d79)



VERILOG CODE:



LOGIC GATES:
~~~
      module gate(a,b,w1,w2,w3,w4,w5,w6,w7);
      input a,b;
      output w1,w2,w3,w4,w5,w6,w7;
      and g1 (w1,a,b);
      or g2 (w2,a,b);
      not g3 (w3,a);
      xor g4 (w4,a,b);
      xnor g5 (w5,a,b);
      nand g6 (w6,a,b);
      nor g7 (w7,a,b);
      endmodule
~~~



OUTPUT:


![image](https://github.com/thrishag/VLSI-LAB-EXP-1/assets/98105360/4a6fc716-61a1-407f-9b0f-05d3a22665d2)



FULL ADDER:
~~~
       module fulladder(a,b,cin,sum,carry);
       input a,b,cin;
       output sum,carry;
       wire w1,w2,w3;
       xor g1(w1,a,b);
       xor g2(sum,w1,cin);
       and g3(w2,w1,cin);
       and  g4(w3,a,b);
       or g5(carry,w2,w3);
       endmodule
~~~



OUTPUT:


![image](https://github.com/thrishag/VLSI-LAB-EXP-1/assets/98105360/a3d55d7b-7e85-4547-a15a-695b827f09ee)



HALF ADDER:
~~~
        module hs(a,b,difference,borrow);
       input a,b;
       output difference,borrow;
       wire w;
       xor g1(difference,a,b);
       and g2(borrow,w,b);
       not g3(w,a);
       endmodule
~~~



OUTPUT:



![image](https://github.com/thrishag/VLSI-LAB-EXP-1/assets/98105360/1aa23c74-d08b-468a-a9b7-89c5131bd9c2)



HALF SUBTRACTOR:
~~~

module hs(a,b,difference,borrow);
       input a,b;
       output difference,borrow;
       wire w;
       xor g1(difference,a,b);
       and g2(borrow,w,b);
       not g3(w,a);
       endmodule
~~~



OUTPUT:


![image](https://github.com/thrishag/VLSI-LAB-EXP-1/assets/98105360/e4b540f1-8c08-4659-97fc-ccd1a304a8cb)



FULL SUBTRACTOR:
~~~
module fs(a,b,c,diff,borrow);
    input a,b,c;
    output diff,borrow;
    wire w1,w2,w3,w4,w5;
    xor g1(w3,a,b);
    xor g2(diff,c,w3);
    and g3(w2,b,w1);
    and g4(w5,w4,c);
    not g5(w1,a);
    not g6(w4,w3);
    nor g7(borrow,w5,w2);
    endmodule   
~~~



OUTPUT:



![image](https://github.com/thrishag/VLSI-LAB-EXP-1/assets/98105360/8a59587e-a839-4b3c-95ac-ff40d1619829)



8 RIPPLE CARRY ADDER

~~~
module fa(a,b,c,sum,carry);
input a,b,c;
output sum,carry;
assign sum = a^b^c;
assign carry=(a&b)|(b&c)|(c&a);
endmodule
module rca(a,b,cin,sum,cout);
input [7:0]a,b;
input cin;
output [7:0]sum;
output cout;
wire c1,c2,c3,c4,c5,c6,c7;
fa fa1(a[0],b[0],cin,sum[0],c1);
fa fa2(a[1],b[1],c1,sum[1],c2);
fa fa3(a[2],b[2],c2,sum[2],c3);
fa fa4(a[3],b[3],c3,sum[3],c4);
fa fa5(a[4],b[4],c4,sum[4],c5);
fa fa6(a[5],b[5],c5,sum[5],c6);
fa fa7(a[6],b[6],c6,sum[6],c7);
fa fa8(a[7],b[7],c7,sum[7],cout);
endmodule

           
~~~



OUTPUT:



![image](https://github.com/thrishag/VLSI-LAB-EXP-1/assets/98105360/c5bfd9db-edc8-4037-8698-ffb09f654648)




RESULT:
       Hence, the stimulation and synthesis of a Logic Gates,Adders and Subtractor was run successfully by using Xilinx ISE.
