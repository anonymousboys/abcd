er=2.3;
ur=1;
d=0.9*(10.^-3);
D=3.15*(10.^-3);
sigmad=1.2*(10.^-12);
sigmac=6*(10.^7);
fo=2.4*(10.^9);
eo=8.854*(10.^-12);
uo=4*pi*(10.^-7);
C=2*pi*eo*er/(log(D/d)); %Capacitance
L=uo*ur*log(D/d)/(4*pi); %Inductance
R=4/(sigmac*pi*d*d); %Resistance
G=sigmad*pi*((D*D)-(d*d))/4; %Conductance
Y=((R+1i*2*pi*fo*L)*(G+1i*2*pi*fo*C))^-0.5; %Propagation Constant
Zo=((R+1i*2*pi*fo*L)/(G+1i*2*pi*fo*C))^-0.5;
disp("The Primary Constants are:");
fprintf("Resistance = %f\n", R);
fprintf("Capacitance = %d\n", C);
fprintf("Inductance = %d\n", L);
fprintf("Conductance = %d\n\n", G);
disp("The Secondary Constants are:");
fprintf("Propagation Constant = %f + %f j\n", real(Y), imag(Y));
fprintf("Characteristic Impedance = %f + %f j\n", real(Zo), imag(Zo));
