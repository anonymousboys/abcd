c=3e8;
Z_0=100;
l=0.2054;
a=0;
R_s=Z_0;
L_s=4e-9;
C_s=0.5e-12;
f_range=1e9:5e6:8e9;
num=(8e9-1e9)/5e6;
Z_L=zeros(num,1);
Z_in=zeros(num,1);
reflect=zeros(num,1);
swr=zeros(num,1);
x=1;
for f=f_range
w=2*pi*f;
B=w/c;
Z_L(x)=R_s+1i*w*L_s+1/(1i*w*C_s);
Z_in(x)=Z_0*((Z_L(x)+1i*Z_0*tan(B*1))/(Z_0+1i*Z_L(x)*tan(B*1)));
reflect(x)=(Z_L(x)-Z_0)/(Z_L(x)+Z_0);
swr(x)= abs((1+reflect(x))/(1-reflect(x)));
x=x+1;
end
figure('Name','VSWR vs Frequency')
plot(f_range, swr);
title("VSWR vs Frequency");
xlabel("frequency (Hz)");
ylabel("VSWR");
