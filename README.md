# Four_Bit_Multiplier
A four-bit multiplier is a digital circuit used to multiply two four-bit binary numbers. It performs partial multiplications, shifting, and adding to obtain an eight-bit output. It's an essential component in digital systems and microprocessors for arithmetic operations, enabling efficient binary multiplication.


## VHDL Code


module Bit_multiplier_4(o,a,b);  
input [3:0] a,b;    
output [8:1] o;  
wire [32:1] w;  
assign o[1]= a[0] & b[0];  
assign w[1]= a[1] & b[0];  
assign w[2]= a[0] & b[1];  
assign w[4]= a[2] & b[0];  
assign w[5]= a[1] & b[1];  
assign w[8]= a[0] & b[2];  
assign w[10]= a[3] & b[0];  
assign w[15]= a[2] & b[1];  
assign w[16]= a[1] & b[2];  
assign w[17]= a[0] & b[3];  
assign w[21]= a[3] & b[1]; 
assign w[22]= a[2] & b[2];  
assign w[25]= a[1] & b[3];  
assign w[30]= a[3] & b[2];  
assign w[31]= a[2] & b[3];  
assign w[32]= a[3] & b[3];  
half_adder h1(o[2],w[3],w[1],w[2]);  
half_adder h2(o[3],w[9],w[6],w[8]);   
half_adder h3(o[4],w[18],w[13],w[17]);  
half_adder h4(o[5],w[26],w[23],w[25]);    
full_adder f1(w[6],w[7],w[3],w[4],w[3] ,w[5]);  
full_adder f2(w[11],w[12],w[7],w[10] ,w[9]);  
full_adder f3(w[13],w[14],w[11],w[15] ,w[16]);  
full_adder f4(w[19],w[20],w[12],w[14] ,w[18]);  
full_adder f5(w[23],w[24],w[20],w[21] ,w[22]);  
full_adder f6(w[27],w[28],w[24],w[26] ,w[20]);   
full_adder f7(o[6],w[29],w[27],w[30] ,w[31]);   
full_adder f8(o[7],o[8],w[32],w[28] ,w[29]);    
endmodule     
module half_adder(S,C,A,B);   
input A,B;   
output S,C;    
xor_gate x1 (S,A,B);   
and (C,A,B);   
endmodule   
module xor_gate(D,A,B);   
input A,B;   
output D;    
wire [3:0] w;   
not (w[0],A);   
not (w[1],B);      
and (w[2],w[0],B);    
and (w[3],A,w[1]);    
or (D,w[2],w[3]);    
endmodule    
module full_adder(sum,carry,a,b,Cin);    
input a,b,Cin;    
output sum,carry;   
wire w1,w2,w3;       
half_adder Ha1 (w1,w2,a,b);   
half_adder Ha2 (sum,w3,w1,Cin);   
or (carry,w3,w2);   
endmodule   
