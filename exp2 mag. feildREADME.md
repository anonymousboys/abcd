clc;
clear all;
close all;
d=0.30;
L=20;
k=5;
ks=k*[0 1 0];
Xmin=-0.15;
Xmax=0.15;
Ymin=-10;
Ymax=10;
no_of_Xdivisions =20;
no_of_Ydivisions=100;
dx=(Xmax-Xmin)/no_of_Xdivisions;
dy=(Ymax-Ymin)/no_of_Ydivisions;
ds=dx*dy;
ZCellCentre=0;
Number_of_X_Plotting_Points=10;
Number_of_Z_Plotting_Points=10;
PlotXmin=-0.5;
PlotXmax=0.5;
PlotZmin=-0.5;
PlotZmax=0.5;
PlotStepX=(PlotXmax-PlotXmin)/(Number_of_X_Plotting_Points-1);
PlotStepZ=(PlotZmax-PlotZmin)/(Number_of_Z_Plotting_Points-1);
[XData,ZData]=meshgrid(PlotXmin:PlotStepX:PlotXmax,PlotZmin:PlotStepZ:PlotZmax);
PlotY=0;
Bx=zeros(Number_of_X_Plotting_Points, Number_of_Z_Plotting_Points);
Bz=zeros(Number_of_X_Plotting_Points, Number_of_Z_Plotting_Points);
for m=1:Number_of_X_Plotting_Points
for n=1:Number_of_Z_Plotting_Points
PlotX=XData(m,n);
PlotZ=ZData(m,n);
if((PlotZ==0)&(PlotX>=Xmin)&(PlotX<=Xmax))
Bx(m,n)=0.5*k;
Bz(m,n)=0;
continue;
end
Rp=[PlotX PlotY PlotZ];
for i=1:no_of_Xdivisions
for j=1:no_of_Ydivisions
XCellCentre=Xmin+(i-1)*dx+0.5*dx;
YCellCentre=Ymin+(j-1)*dy+0.5*dy;
Rc=[XCellCentre YCellCentre ZCellCentre];
R=Rp-Rc;
norm_R=norm(R);
R_Hat=R/norm(R);
dH=(ds/(4*pi*norm_R*norm_R))*cross(ks,R_Hat);
Bx(m,n)=Bx(m,n)+dH(1,1);
Bz(m,n)=Bz(m,n)+dH(1,3);
end
end
end
end
quiver(XData,ZData,Bx,Bz);
xlabel('z axis');
ylabel('x axis');
title('field lines in x-z plane');
P=[0 0 0.25];
H=[0 0 0];
for i=1:no_of_Xdivisions
for j=1:no_of_Ydivisions
XCellCentre=Xmin+(i-1)*dx+0.5*dx;
YCellCentre=Ymin+(j-1)*dy+0.5*dy;
Rc=[XCellCentre YCellCentre ZCellCentre];
R=P-Rc;
norm_R=norm(R);
R_Hat=R/norm(R);
dH=(ds/(4*pi*norm_R*norm_R))*cross(ks,R_Hat);
H=H+dH;
end
end
