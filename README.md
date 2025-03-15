# DAY-48_100_DAYS_OF_RTL
//WALLACE TREE MULTIPLIER ALGORITHM

module WallaceMultiplier (input [3:0] A, input [3:0] B, output [7:0] Product);
    wire [3:0] pp0, pp1, pp2, pp3;
    wire [4:0] sum1, carry1;
    wire [5:0] sum2, carry2;
    wire [6:0] sum3, carry3;
    
    assign pp0 = A & {4{B[0]}};
    assign pp1 = A & {4{B[1]}};
    assign pp2 = A & {4{B[2]}};
    assign pp3 = A & {4{B[3]}};
    
    assign sum1 = {pp1, 1'b0} + {1'b0, pp0};
    assign carry1 = {pp1, 1'b0} & {1'b0, pp0};
    
    assign sum2 = {pp2, 2'b00} + {carry1, 1'b0};
    assign carry2 = {pp2, 2'b00} & {carry1, 1'b0};
    
    assign sum3 = {pp3, 3'b000} + {carry2, 1'b0};
    assign carry3 = {pp3, 3'b000} & {carry2, 1'b0};
    
    assign Product = sum3 + {carry3, 1'b0};
endmodule

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

module WallaceMultiplier_tb;
    reg [3:0] A, B;
    wire [7:0] Product;
    
    WallaceMultiplier uut (A, B, Product);
    
    initial begin
        $monitor("A = %b, B = %b, Product = %b", A, B, Product);
        
        A = 4'b1011; B = 4'b1101; #10;
        A = 4'b0110; B = 4'b0101; #10;
        A = 4'b0111; B = 4'b0011; #10;
        A = 4'b0011; B = 4'b1010; #10;
        
        $finish;
    end
endmodule
