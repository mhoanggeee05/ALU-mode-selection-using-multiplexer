module addsubfun (
	input [7:0] A,
	input [7:0] B,
	input clock,
	input reset,
	input [2:0] sel,
	output ovf,
	output co,
	output [7:0] D0
	);
	
	wire tempco;
	wire add_sub;
	EBA u2 (.A(A),.B(B),.S(D0),.M(add_sub),.Co(tempco),.ovf(ovf));
	
	assign co = tempco^add_sub;
	assign add_sub = ~sel[2] &~sel[1] &sel[0];


endmodule

 module EBA (
	input logic [7:0] A,
	input logic [7:0] B,
	input logic M,
	output logic [7:0] S,
	output logic Co,
	output logic ovf
	);
logic [6:0] temp;

	FA u0 (.a(A[0]),.b(B[0]^M),.ci(M),.s(S[0]),.co(temp[0]));
	FA u1 (.a(A[1]),.b(B[1]^M),.ci(temp[0]),.s(S[1]),.co(temp[1]));
	FA u2 (.a(A[2]),.b(B[2]^M),.ci(temp[1]),.s(S[2]),.co(temp[2]));
	FA u3 (.a(A[3]),.b(B[3]^M),.ci(temp[2]),.s(S[3]),.co(temp[3]));
	FA u4 (.a(A[4]),.b(B[4]^M),.ci(temp[3]),.s(S[4]),.co(temp[4]));
	FA u5 (.a(A[5]),.b(B[5]^M),.ci(temp[4]),.s(S[5]),.co(temp[5]));
	FA u6 (.a(A[6]),.b(B[6]^M),.ci(temp[5]),.s(S[6]),.co(temp[6]));
	FA u7 (.a(A[7]),.b(B[7]^M),.ci(temp[6]),.s(S[7]),.co(Co));
	assign ovf = Co^temp[6];
		
endmodule

	
module FA (
	input logic a,b,ci,
	output logic s, co
   );
	
	assign s = a^b^ci;
	assign co=a&b|ci&a|ci&b;
	
endmodule

module shiftleft (
	input [7:0] A, B,
	input clk,
	input rst,
	output [7:0] D1
	);
	
	shiftregleft u2(.A(A),.B(B),.P(D1));
	
endmodule
	
module shiftregleft (
	input [7:0] A, B,
	output [7:0] P
	);
	
	logic [7:0] temp;
	
	MUX u0 (.D0(A[0]),.D1(1'b0),.D2(1'b0),.D3(1'b0),.D4(1'b0),.D5(1'b0),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[0]));
	MUX u1 (.D0(A[1]),.D1(A[0]),.D2(1'b0),.D3(1'b0),.D4(1'b0),.D5(1'b0),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[1]));
	MUX u2 (.D0(A[2]),.D1(A[1]),.D2(A[0]),.D3(1'b0),.D4(1'b0),.D5(1'b0),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[2]));
	MUX u3 (.D0(A[3]),.D1(A[2]),.D2(A[1]),.D3(A[0]),.D4(1'b0),.D5(1'b0),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[3]));
	MUX u4 (.D0(A[4]),.D1(A[3]),.D2(A[2]),.D3(A[1]),.D4(A[0]),.D5(1'b0),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[4]));
	MUX u5 (.D0(A[5]),.D1(A[4]),.D2(A[3]),.D3(A[2]),.D4(A[1]),.D5(A[0]),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[5]));
	MUX u6 (.D0(A[6]),.D1(A[5]),.D2(A[4]),.D3(A[3]),.D4(A[2]),.D5(A[1]),.D6(A[0]),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[6]));
	MUX u7 (.D0(A[7]),.D1(A[6]),.D2(A[5]),.D3(A[4]),.D4(A[3]),.D5(A[2]),.D6(A[1]),.D7(A[0]),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[7]));
	
	logic  B_temp;
	assign B_temp = ~(B[7] | B[6] |B[5] |B[4] |B[3]);
	assign P[0] = B_temp & temp[0];
	assign P[1] = B_temp & temp[1];
	assign P[2] = B_temp & temp[2];
	assign P[3] = B_temp & temp[3];
	assign P[4] = B_temp & temp[4];
	assign P[5] = B_temp & temp[5];
	assign P[6] = B_temp & temp[6];
	assign P[7] = B_temp & temp[7];
	
endmodule

module MUX (
	input logic D7, D6, D5, D4, D3, D2, D1, D0,
	input logic S2, S1, S0,
	output logic Y
	);
	assign Y = (~S2 &~S1 &~S0 &D0 | ~S2 &~S1 &S0 &D1) |
				  (~S2 & S1 &~S0 &D2 | ~S2 & S1 &S0 &D3) |
				  (S2 &~S1 &~S0 &D4 |  S2 &~S1 &S0 &D5)  |
				  (S2 & S1 &~S0 &D6 |  S2 & S1 &S0 &D7)   ;

endmodule

module shiftright (
	input [7:0] A, B,
	input clk,
	input rst,
	output [7:0] D2
	);
	
	shiftregright u2(.A(A),.B(B),.P(D2));
	
endmodule
	
module shiftregright (
	input [7:0] A, B,
	output [7:0] P
	);
	
	logic [7:0] temp;
	
	MUX u0 (.D0(A[0]),.D1(A[1]),.D2(A[2]),.D3(A[3]),.D4(A[4]),.D5(A[5]),.D6(A[6]),.D7(A[7]),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[0]));
	MUX u1 (.D0(A[1]),.D1(A[2]),.D2(A[3]),.D3(A[4]),.D4(A[5]),.D5(A[6]),.D6(A[7]),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[1]));
	MUX u2 (.D0(A[2]),.D1(A[3]),.D2(A[4]),.D3(A[5]),.D4(A[6]),.D5(A[7]),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[2]));
	MUX u3 (.D0(A[3]),.D1(A[4]),.D2(A[5]),.D3(A[6]),.D4(A[7]),.D5(1'b0),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[3]));
	MUX u4 (.D0(A[4]),.D1(A[5]),.D2(A[6]),.D3(A[7]),.D4(1'b0),.D5(1'b0),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[4]));
	MUX u5 (.D0(A[5]),.D1(A[6]),.D2(A[7]),.D3(1'b0),.D4(1'b0),.D5(1'b0),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[5]));
	MUX u6 (.D0(A[6]),.D1(A[7]),.D2(1'b0),.D3(1'b0),.D4(1'b0),.D5(1'b0),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[6]));
	MUX u7 (.D0(A[7]),.D1(1'b0),.D2(1'b0),.D3(1'b0),.D4(1'b0),.D5(1'b0),.D6(1'b0),.D7(1'b0),.S2(B[2]),.S1(B[1]),.S0(B[0]),.Y(temp[7]));
	
	logic  B_temp;
	assign B_temp = ~(B[7] | B[6] |B[5] |B[4] |B[3]);
	assign P[0] = B_temp & temp[0];
	assign P[1] = B_temp & temp[1];
	assign P[2] = B_temp & temp[2];
	assign P[3] = B_temp & temp[3];
	assign P[4] = B_temp & temp[4];
	assign P[5] = B_temp & temp[5];
	assign P[6] = B_temp & temp[6];
	assign P[7] = B_temp & temp[7];
	
endmodule
module anding (
	input [7:0] A,B,
	output [7:0] D3
	);
	
	assign D3[0] = A[0] & B[0];
	assign D3[1] = A[1] & B[1];
	assign D3[2] = A[2] & B[2];
	assign D3[3] = A[3] & B[3];
	assign D3[4] = A[4] & B[4];
	assign D3[5] = A[5] & B[5];
	assign D3[6] = A[6] & B[6];
	assign D3[7] = A[7] & B[7];
	
endmodule

module oring (
	input [7:0] A,B,
	output [7:0] D4
	);
	
	assign D4[0] = A[0] | B[0];
	assign D4[1] = A[1] | B[1];
	assign D4[2] = A[2] | B[2];
	assign D4[3] = A[3] | B[3];
	assign D4[4] = A[4] | B[4];
	assign D4[5] = A[5] | B[5];
	assign D4[6] = A[6] | B[6];
	assign D4[7] = A[7] | B[7];
	
endmodule
module xoring (
	input [7:0] A,B,
	output [7:0] D5
	);
	
	assign D5[0] = A[0] ^ B[0];
	assign D5[1] = A[1] ^ B[1];
	assign D5[2] = A[2] ^ B[2];
	assign D5[3] = A[3] ^ B[3];
	assign D5[4] = A[4] ^ B[4];
	assign D5[5] = A[5] ^ B[5];
	assign D5[6] = A[6] ^ B[6];
	assign D5[7] = A[7] ^ B[7];
	
endmodule
module notA (
	input [7:0] A,
	output [7:0] D6
	);
	
	assign D6 = ~A;
	
endmodule 
	module ALU (
	input [7:0] A,B,
	input [2:0] sel,
	input rst,
	input clk,
	output ovf, cout,
	output [7:0] P
	);
	
	wire [7:0] tempD0; 
	wire [7:0] tempD1;
	wire [7:0] tempD2;
	wire [7:0] tempD3;
	wire [7:0] tempD4;
	wire [7:0] tempD5;
	wire [7:0] tempD6;

	addsubfun u0 (.A(A),.B(B),.sel(sel),.reset(rst),.clock(clk),.ovf(ovf),.co(cout),.D0(tempD0));
	shiftleft u1 (.A(A),.B(B),.rst(rst),.clk(clk),.D1(tempD1));
	shiftright u2(.A(A),.B(B),.rst(rst),.clk(clk),.D2(tempD2));
	anding u3 (.A(A),.B(B),.D3(tempD3));
	oring u4 (.A(A),.B(B),.D4(tempD4));
	xoring u5(.A(A),.B(B),.D5(tempD5));
	notA u6(.A(A),.D6(tempD6));
	MUXsort mu0(.D0(tempD0[0]),.D1(tempD1[0]),.D2(tempD2[0]),.D3(tempD3[0]),.D4(tempD4[0]),.D5(tempD5[0]),.D6(tempD6[0]),.D7(1'h0),.S2(sel[2]),.S1(sel[1]),.S0(sel[0]),.Y(P[0]));
	MUXsort mu1(.D0(tempD0[1]),.D1(tempD1[1]),.D2(tempD2[1]),.D3(tempD3[1]),.D4(tempD4[1]),.D5(tempD5[1]),.D6(tempD6[1]),.D7(1'h0),.S2(sel[2]),.S1(sel[1]),.S0(sel[0]),.Y(P[1]));
	MUXsort mu2(.D0(tempD0[2]),.D1(tempD1[2]),.D2(tempD2[2]),.D3(tempD3[2]),.D4(tempD4[2]),.D5(tempD5[2]),.D6(tempD6[2]),.D7(1'h0),.S2(sel[2]),.S1(sel[1]),.S0(sel[0]),.Y(P[2]));
	MUXsort mu3(.D0(tempD0[3]),.D1(tempD1[3]),.D2(tempD2[3]),.D3(tempD3[3]),.D4(tempD4[3]),.D5(tempD5[3]),.D6(tempD6[3]),.D7(1'h0),.S2(sel[2]),.S1(sel[1]),.S0(sel[0]),.Y(P[3]));
	MUXsort mu4(.D0(tempD0[4]),.D1(tempD1[4]),.D2(tempD2[4]),.D3(tempD3[4]),.D4(tempD4[4]),.D5(tempD5[4]),.D6(tempD6[4]),.D7(1'h0),.S2(sel[2]),.S1(sel[1]),.S0(sel[0]),.Y(P[4]));
	MUXsort mu5(.D0(tempD0[5]),.D1(tempD1[5]),.D2(tempD2[5]),.D3(tempD3[5]),.D4(tempD4[5]),.D5(tempD5[5]),.D6(tempD6[5]),.D7(1'h0),.S2(sel[2]),.S1(sel[1]),.S0(sel[0]),.Y(P[5]));
	MUXsort mu6(.D0(tempD0[6]),.D1(tempD1[6]),.D2(tempD2[6]),.D3(tempD3[6]),.D4(tempD4[6]),.D5(tempD5[6]),.D6(tempD6[6]),.D7(1'h0),.S2(sel[2]),.S1(sel[1]),.S0(sel[0]),.Y(P[6]));
	MUXsort mu7(.D0(tempD0[7]),.D1(tempD1[7]),.D2(tempD2[7]),.D3(tempD3[7]),.D4(tempD4[7]),.D5(tempD5[7]),.D6(tempD6[7]),.D7(1'h0),.S2(sel[2]),.S1(sel[1]),.S0(sel[0]),.Y(P[7]));

endmodule
module MUXsort (
	input   D7, D6, D5, D4, D3, D2, D1, D0,
	input logic S2, S1, S0,
	output  Y
	);
assign Y =
      (~S2 & ~S1 & ~S0 & D0) |
		(~S2 & ~S1 &  S0 & D0) |
      (~S2 &  S1 & ~S0 & D1) |
      (~S2 &  S1 &  S0 & D2) |
      ( S2 & ~S1 & ~S0 & D3) |
      ( S2 & ~S1 &  S0 & D4) |
      ( S2 &  S1 & ~S0 & D5) |
      ( S2 &  S1 &  S0 & D6);

endmodule
	module Lab1_ex4(
	input [7:0] datainput,
	input clk,
	input rst,
	input ENA,
	input ENB,
	input [2:0] sel,
	output [7:0] A, B,P,
	output [7:0] dataoutput,
	output ovf, finalcarry
	);
	
	wire tempco;
	wire tempovf;
	nbitregEB u0 (.D(datainput),.rst(rst),.clk(clk),.ENB(ENB),.Q(B));
	nbitregEA u1(.D(datainput),.rst(rst),.clk(clk),.ENA(ENA),.Q(A));
   ALU u2(.A(A),.B(B),.clk(clk),.rst(rst),.ovf(tempovf),.cout(tempco),.sel(sel),.P(P));
	nbitreg u3 (.D(P),.rst(rst),.clk(clk),.Q(dataoutput));
	d_ff D_carry (.D(tempco),.rst(rst),.clk(clk),.Q(finalcarry));
	d_ff D_ovf (.D(tempovf),.rst(rst),.clk(clk),.Q(ovf)); 
	
endmodule
	
module d_ff (
	input logic D,
	input clk,
	input logic rst,
   output logic Q
	);
	
	always_ff @(posedge clk, posedge rst)
		if (rst)
			Q <='b0;
		else
		Q <= D;
	
endmodule 
					
module nbitregEB (
	input logic [7:0] D,
	input logic rst,
	input clk,
	input ENB, 
	output reg [7:0] Q
	);
	
	always_ff @(posedge clk, posedge rst) 
	if (rst) Q <= '0;
	else if (ENB) Q <= D;
endmodule
	
module nbitregEA (
	input logic [7:0] D,
	input logic rst,
	input clk,
	input ENA, 
	output reg [7:0] Q
	);
	
	always_ff @(posedge clk, posedge rst) 
	if (rst) Q <= '0;
	else if (ENA) Q <= D;
	
endmodule

module nbitreg (
	input logic [7:0] D,
	input logic rst,
	input clk,
	output reg [7:0] Q
	);
	
	always_ff @(posedge clk, posedge rst) 
	if (rst) Q <= '0;
	else  Q <= D;
	
endmodule

