module ex4_testbench ();
	logic [7:0] datainput;
	logic clk;
	logic rst;
	logic ENA;
	logic ENB;
	logic [2:0] sel;
	logic [7:0] A;
	logic [7:0] B;
	logic [7:0] P;
	logic [7:0] dataoutput;
	logic ovf; 
	logic finalcarry;
	
	Lab1_ex4 DUT (.datainput(datainput),.clk(clk),.rst(rst),.ENA(ENA),.ENB(ENB),.sel(sel),.A(A),.B(B),.P(P),.dataoutput(dataoutput),.ovf(ovf),.finalcarry(finalcarry));
	
	always
	begin
			clk=1;#5;
			clk=0;#5;
	end
	
	initial
	begin 
			rst=1;datainput=8'h0;ENA=0;ENB=0;sel=0;
			#5; rst=0;datainput=8'h70;ENA=1;
			#7; ENA=0;ENB=1;
			#3; datainput = 8'h25;
			#7; sel=3'h1; 
			#3; datainput= 8'h4A;
			#7; ENA=1; ENB=0; sel=3'h2;
			#3; datainput=8'hAC;
			#7; ENA=0; ENB=1;
			#3; datainput = 8'h03;
			#7; sel=3'h3;
			#3; datainput=8'h05;
			#7; ENA=1; ENB=0; sel=3'h4;
			#3; datainput = 8'h9A;
			#7; ENB=1;
			#3; datainput=8'h28;
			#7; ENA=0;sel=3'h5;
			#3; datainput=8'h67;
			#7; sel=3'h5;
			#3; datainput = 8'h89;
			#7; sel=3'h6;
			#3; datainput = 8'hFA;
			#7; sel = 3'h7;
	end
endmodule
			
			
